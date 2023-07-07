# Airflow

출처 [Airflow 공식문서](https://airflow.apache.org/docs/apache-airflow/stable/index.html)

- Apache 라이센스를 가지고 있는 Workflow Management Tool.
- workflow 작성 / 스케줄링 / 모니터링 수행.
- workflow를 빌드하고 실행할 수 있게 하는 플랫폼.
- 하나의 workflow는 DAG로 표현.

## 구성 요소

- WebServer : 사용자에게 UI 제공.
- Scheduler : DAG Directory에서 작성된 DAG를 읽어와 workflow를 triggering하고, task를 Executor에 제공.
- Executor : 
- Workers : 실제 task을 실행.
- DAG Directory : DAG이 저장되는 디렉토리.
- Metadata Database : DAG와 Task의 정보, 실행상태 등을 저장.

## DAG(Directed Acyclic Graph)

- 반복이나 순환하지 않는 그래프(워크플로우)
- Task와 Operator의 정의와 Task의 순서를 정의

```python
from airflow import DAG
from airflow.decorators import task
from airflow.operators.bash import BashOperator

with DAT(
    dag_id = "demo",
    start_date = datetime(2023, 6, 6),
    schedule = "0 0 * * *"
) as dag;

task1 = BashOperator(
    task_id = "task1",
    bash_command = "echo hello task1"
);
@task
def airflow():
    print("hello airflow")

task1 >> airflow()
```

## Operator

- Task 정의


## 동작 원리
1. 개발자 및 사용자가 DAG 작성
2. Scheduler가 DAG Directory에 있는 DAG를 읽어와 Workflow 생성
3. 