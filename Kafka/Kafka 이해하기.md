# 카프카란?
- 아파치 재단의 카프카는 pub-sub 모델의 메세지 큐
- 분산환경에 특화되어 설계됨
- 기존의 RabbitMQ와 같은 다른 메세지큐와의 성능 차이가 남
- 그 외 클러스터 구성, fail-over, replication과 같은 여러 가지 특징을 가짐

## Pub-Sub 모델
- 카프카는 pub-sub(발행/구독) 모델을 사용
- pub-sub은 메세지를 특정 수신자에게 직접적으로 보내주는 시스템이 아님
- publisher는 메세지를 topic을 통해서 카테고리화 함
- 분류된 메세지를 받기 원하는 receiver는 해당 topic을 구독(subscribe)함으로써 메세지를 읽어 올 수 있음
- 즉, publisher는 topic에 대한 정보만 알고, subscriber도 topic만 바라봄
- publisher와 subscriber는 서로 모르는 상태
- 예를들면, 신문사에서 신문의 종류(topic)에 메세지를 쓴다. 우리는 그 해당 신문을 구독 한다.

```
카프카의 구성요소 및 특징
- topic, parition
- Producer, Consumer
- broker, zookeeper
- consumer group
- replication
```

### 참고
- [카프카 이해하기](https://medium.com/@umanking/%EC%B9%B4%ED%94%84%EC%B9%B4%EC%97%90-%EB%8C%80%ED%95%B4%EC%84%9C-%EC%9D%B4%EC%95%BC%EA%B8%B0-%ED%95%98%EA%B8%B0%EC%A0%84%EC%97%90-%EB%A8%BC%EC%A0%80-data%EC%97%90-%EB%8C%80%ED%95%B4%EC%84%9C-%EC%9D%B4%EC%95%BC%EA%B8%B0%ED%95%B4%EB%B3%B4%EC%9E%90-d2e3ca2f3c2)