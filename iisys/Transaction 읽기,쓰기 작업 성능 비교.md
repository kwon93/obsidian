

##### transaction 읽기와 쓰기는 나누지 않았을때
- transaction 완료까지의 시간 : 62.569ms
	- transaction{읽기, 읽기, 쓰기, 읽기, 읽기, 쓰기}

##### transaction 읽기와 쓰기를 분리했을 때
- transaction 완료까지의 시간: 47.179ms
	- 읽기, 읽기 transaction{ 쓰기, 읽기, 읽기, 쓰기}
		- (첫번째 쓰기의 결과값을 이용한 읽기 작업은 transaction에 포함)

##### 24.6%의 성능 향상
- **트랜잭션 범위 축소 효과** 트랜잭션에 포함된 작업이 줄어들면 트랜잭션이 유지되는 시간이 줄어듭니다. 첫 두 번의 읽기 작업을 트랜잭션 외부로 이동시킴으로써, 데이터베이스가 트랜잭션 상태를 관리하는 시간이 단축되었습니다.
- **잠금 경합 감소** REPEATABLE_READ 격리 수준에서는 읽기 작업도 특정 형태의 잠금을 유발할 수 있습니다. 읽기 작업을 트랜잭션 밖으로 이동시킴으로써, 다른 트랜잭션과의 잠금 경합 가능성이 감소했습니다.
- **데이터베이스 리소스 효율성** 트랜잭션은 데이터베이스 엔진에 추가 부담을 줍니다. 각 작업이 트랜잭션 로그에 기록되고, 일관성을 보장하기 위한 추가 검사가 수행됩니다. 트랜잭션 범위를 좁힘으로써 이러한 오버헤드가 감소합니다.


#### But
트랜잭션을 읽기와 쓰기로 분리하는 것이 항상 더 나은 것은 아닙니다. 분리의 적합성은 구체적인 사용 사례와 데이터 접근 패턴에 따라 달라집니다.
- **동시성 문제 증가**: 읽기와 쓰기 사이에 다른 트랜잭션이 데이터를 변경할 수 있습니다. 이로 인해 "lost update" 또는 "phantom read" 같은 문제가 발생할 수 있습니다.
- **데이터 일관성 문제**: 트랜잭션을 분리하면 읽은 데이터와 수정하려는 데이터 사이에 불일치가 발생할 위험이 있습니다. 예를 들어, 가장 가까운 브래킷을 찾은 후 트랜잭션이 끝나고, 쓰기 트랜잭션이 시작되기 전에 다른 세션이 관련 브래킷을 수정하면 문제가 발생합니다.

CAP 정리(Consistency, Availability, Partition tolerance)와 유사한 개념으로 볼 수 있습니다.
### 트랜잭션 관리의 근본적인 딜레마

데이터베이스 시스템에서는 일반적으로 다음 세 가지 목표를 동시에 완벽하게 달성할 수 없습니다:

1. **높은 동시성(High Concurrency)**: 많은 사용자가 동시에 시스템을 사용할 수 있는 능력
2. **완벽한 데이터 일관성(Perfect Consistency)**: 모든 트랜잭션이 항상 정확하고 일관된 데이터를 보게 함
3. **최대 성능(Maximum Performance)**: 최소한의 지연 시간과 최대 처리량


### 일관성 우선 시스템

- 은행 거래 시스템
- 항공권 예약 시스템
- 재고 관리 시스템
- 의료 기록 시스템

### 성능 우선 시스템

- 소셜 미디어 피드
- 분석 대시보드
- 대용량 로깅 시스템
- 콘텐츠 추천 시스템