## 1. 새로운 할인 정책 개발 ~ 2. 새로운 할인 정책 적용과 문제점

문제점

### OCP, DIP 위반 why?

항상 추상화에 의존해야 하지만 현재는 추상화와 구현 모두에 의존하고 있는 상태 -> **DIP 위반**

```java
private final DiscountPolicy discountPolicy = new FixDiscountPolicy();
private final DiscountPolicy discountPolicy = new RateDiscountPolicy();
```

또한 해당 코드를 고치려면 OrderServiceImpl 에 접근하여 코드수정을 해야함 -> **OCP 위반**

### 어떻게 해결할 수 있을까?

- 클라이언트 코드인 ```OrderServiceImpl``` 은 ```DiscountPolicy``` 의 인터페이스 뿐만 아니라 구현 클래스도 같이 의존한다.
- 그래서 구체 클래스를 변경할 때 클라이언트 코드도 같이 변경해야 한다. -> OCP 위반
- **DIP 위반** -> 추상에만 의존하도록 변경
- DIP를 위반하지 않도록 인터페이스에만 의존하도록 의존관계를 변경하면 된다.

인터페이스에만 의존하도록 설계와 코드를 변경했다.
**그런데 구현체가 없는데 어떻게 코드를 실행할 수 있을까?**
**실제 실행을 해보면 NPE(null pointer exception)가 발생한다.**

### 해결방안

이 문제를 해결하려면 누군가가 클라이언트인 OrderServiceImpl 에 DiscountPolicy 의 구현 객체를 대신 생성하고 주입해주어야 한다.



## 3. 관심사의 분리

