# Multer
multipart/form-data 형식의 단일 및 다중 파일 업로드를 지원하는 미들웨어

## 0. 설치
```bash
npm install multer
# or 
yarn add multer
```

## 1. 적용

multer로 diskStorage에서 경로 설정 시 해당 경로의 디렉토리 필수  

```javascript
const express = require('express');
const multer = require('multer');
const fs = require('fs');

const app = express();

// multer > diskStorage > defination에서 설정한 경로가 필요
try {
  fs.readdirSync('uploads');
} catch(err) {
  fs.mkdirSync('uploads');
}

const uploader = multer({
    storage: multer.diskStorage({
        detination(req, file, done) {
            done(null, 'uploader/');    // done(err, path)
        },
        filename(req, file, done) {
            const ext = path.extname(file.originalname);
            done(null, path.basename(file.originalname, ext) + Date.now() + ext);
        }
    }),
    limits: { fileSize: 5 * 1024 * 1024 }
});

```

- storage(or dest): detination(어디에), filename(파일이름) 설정.
  - diskStorage
    - destination: 저장할 위치. (*필수: 해당 위치가 존재)
    - filename: 저장될 파일 이름.
  - memoryStorage: 메모리에 buffer 객체로 저장.
- limits: 업로드의 제한 사항
  - fieldNameSize: 
  - fieldSize: 
  - fields: 
  - fileSize: 
  - files: 
  - parts: 
  - headerPairs: 
- fileFilter: 허용할 파일 제어

### 단일 파일 업로드

```javascript
app.post('/upload', uploader.single('file'), (req, res) => {
  res.send('success');
});
```

업로드 후 req.file 객체 생성.  
파일 외 데이터는 req.body.

```javascript
// req.file
{
  fieldname: 'html에서 정의된 필드 명',
  originalname: '업로드한 파일 명',
  encoding: '',
  mimetype: '파일 타입',
  destination: '업로드 경로',
  filename: '저장된 파일 명',
  path: '업로드 경로/저장된 파일 명',
  size: '파일 크기(byte)'
}
```

### 다중 파일 업로드

```javascript
app.post('/upload', uploader.array('files'), (req, res) => {
  res.send('success');
})

// or
app.post('/upload', uploader.fields([{ name: 'file1' }, { name: 'file2' }]), (req, res) => {
  res.send('success');
});
```

- array : 업로드 후 req.files 객체 생성.
- fields : 업로드 후 req.files.file1, req.files.file2 생성.

### None 파일

```javascript
app.post('/upload', uploader.none(), (req, res) => {
  res.send('success');
});
```

req.body 만 존재.