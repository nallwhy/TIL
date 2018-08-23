# Transaction

## ACID

### Atomicity

Transaction 내의 모든 statements 가 성공하면 성공, 아니면 실패하고 모두 무효화 된다.

### Consistency

Transaction 이 끝날 때 constrants 는 true 로 유지된다.

### Isolation

Transaction 간에는 간섭을 최소화한다. 서로 관계가 없는 transaction 은 완전히 분리되어있다.
완전 분리는 여러 transaction 이 동시에 일어나더라도, transaction 들을 동시에 실행하는 것과 하나하나 실행하는 것의 결과가 같은 순서가 있다는 의미다.

### Durability

Commit 된 데이터는 항상 보존한다.


## Postgres Transactions Aren’t Fully Isolated

### SELECT

**SELECT** 를 할 때 마다 당시의 snapshot 을 대상으로 실행되는데, 이 때문에 한 transaction 내에서도 같은 select 는 서로 다른 snapshot 을 대상으로 실행되어 다른 결과를 가질 수 있다.

### UPDATE and DELETE

**UPDATE**, **DELETE** 도 **WHERE** 조건에 맞는 row 를 찾기 위해 실행 전에 snapshot 을 한다.
실행 대상이 될 row 들을 찾고 나면 lock 을 시도하는데, 이미 lock 이 되어있다면 lock 이 풀릴 때까지 기다린다.
lock 을 걸고 있던 transaction 이 실패하면 조건에 맞는 row 들을 그대로 가져가고, 성공하면 변경된 row 에 대해 **WHERE** 조건을 다시 확인한다.


Reference:
http://malisper.me/transactions-in-postgres/
http://malisper.me/postgres-transactions-arent-fully-isolated/
