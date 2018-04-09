# MongoDB 

## MongoDB Command

- mongoDB dump

```
mongodump --host 127.0.0.1
```
- mongod DB Object Id 구조
```
첫 번째 4 바이트 타임 스탬프
머신 코드의 다음의 3 바이트는
즉시 프로세스 ID로 구성이 바이트 (PID)
임의의 숫자의 마지막 3 바이트. ( PHP mongodb 드라이버의 경우 순차 증가 )

```