# BackEnd

## 회원 리포지토리 개발

### 회원 리포지토리 코드

- 기능 설명
	findOne() :
	find()와의 차이점은 find()는 documents의 리스트를 반환하고, findOne()은 documents
    객체 하나를 반환한다.


#### MemberService

![](https://velog.velcdn.com/images/beomgeun/post/6ab8ace4-7eee-41a6-8994-087e56aef593/image.png)

- @Transactional : 트랜잭션, 영속성 컨텍스트
- readOnly=true :
1. 데이터의 변경이 없는 읽기 전용 메서드에 사용, 영속성 컨텍스트를 플러시 하지 않으므로 약간의
성능 향상(읽기 전용에는 다 적용)
2. 데이터베이스 드라이버가 지원하면 DB에서 성능 향상
- @Autowired:생성자 Injection 많이 사용, 생성자가 하나면 생략 가능


#### MemberServiceTest

![](https://velog.velcdn.com/images/beomgeun/post/bc695746-5ec5-44b2-90d5-54382cc21abd/image.png)

- 기술 설명
1. @RunWith(SpringRunner.class) : 스프링과 테스트 통합
2. @SpringBootTest : 스프링 부트를 띄우고 테스트(이게 없으면 @Autowired 모두 실패)
3. @Transactional : 반복 가능한 테스트 지원, 각각의 테스트를 실행할 때마다 트랜잭션을시작하고 테스트가 끝나면 트랜잭션을 강제로 롤백
(해당 어노테이션이 테스트 케이스에서 사용될 때만 롤백)

📌 테스트 케이스를 위한 설정
> 테스트는 케이스 격리된 환경에서 실행하고, 끝나면 데이터를 초기화하는 것이 좋다. 그런 면에서 메모리 DB를 사용하는 것이 가장 이상적이다.
추가로 테스트 케이스를 위한 스프링 환경과, 일반적으로 애플리케이션을 실행하는 환경은 보통 다르므로 설정 파일을 다르게 사용.


> 1. addStock() 메서드는 파라미터로 넘어온 수만큼 재고를 늘린다. 이 메서드는 재고가 증가하거나 상품주문을 취소해서 재고를 다시 늘려야 할 때 사용한다.

```
public void addStock(int quantity) {
 this.stockQuantity += quantity;
} 									// 상품 증가
```
