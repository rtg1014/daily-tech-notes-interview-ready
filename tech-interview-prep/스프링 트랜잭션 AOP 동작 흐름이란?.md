## 스프링 트랜잭션 AOP 동작 흐름

- @Transactional어노테이션을 사용한 선언적 트랜잭션 관리(Declarative Transaction Management)의 전체 흐름에는 크게 3가지 요소가 등장합니다. 트랜잭션 매니저, 트랜잭션 AOP 프록시, 트랜잭션 동기화 매니저가 이에 해당됩니다.

- 클라이언트 코드로부터 요청이 들어오면 트랜잭션 AOP 프록시가 트랜잭션 매니저를 획득하고, 트랜잭션을 시작하기 위해서 트랜잭션 매니저에게 요청합니다.
- 트랜잭션 시작 요청 받은 트랜잭션 매니저는 데이터소스를 통해 커넥션을 받아오고 트랜잭션을 시작합니다. 그리고, 트랜잭션 매니저는 트랜잭션이 시작된 커넥션을 동기화 매니저에 보관합니다.
- 이후 트랜잭션이 종료되는 경우 트랜잭션 매니저는 트랜잭션 동기화 매니저에 보관한 커넥션을 가져와 트랜잭션을 종료하고 커넥션을 반환하거나 종료합니다.



## 트랜잭션 매니저와 트랜잭션 동기화 매니저가 무엇인가요? 
- JDBC를 사용한 트랜잭션 관리 코드와 JPA를 사용한 트랜잭션의 양상이 다릅니다.
- 스프링은 개발자가 트랜잭션에 대한 구현 세부 사항을 신경 쓰지 않도록 트랜잭션 추상화인 PlatformTransactionManager를 제공합니다.
- 개발자는 상황에 맞게 DataSourceTransactionManager, JpaTransactionManager를 사용할 수 있으며, 이를 트랜잭션 매니저(Transaction Manager) 라고 부릅니다.

<br>


서비스 로직에서 여러 서비스 로직을 호출할 수 있고, 데이터 접근 로직을 호출할 수도 있습니다. 이때 트랜잭션을 유지하기 위해서는 해당 트랜잭션을 시작한 커넥션이 여러 코드에 걸쳐 필요하게 됩니다. 트랜잭션 동기화 매니저(Transaction Syncronization Manager) 는 이를 도와줍니다. 만약, 트랜잭션 동기화 매니저가 없다면, 다른 코드의 메서드를 호출할 때마다 커넥션을 인자로 넘겨줘야 하는 문제가 발생합니다.

<br>

---
---


<br>


> ## 추가 학습자료

[10분 테코톡] 기론, 리버의 JDK Dynamic Proxy와 CGLIB
출처 : https://www.youtube.com/watch?v=MFckVKrJLRQ



### **📌 스프링과 프록시: 이해하기 쉽게 풀어보기**  
📢 **"AOP(Aspect-Oriented Programming)를 이해하려면 프록시부터 알아야 한다!"**  
이번 발표에서는 **스프링에서 프록시가 어떻게 활용되는지** 이해하기 쉽게 설명해보겠습니다.  

---

# **📌 목차**
1️⃣ **프록시란?**  
2️⃣ **정적 프록시 vs 동적 프록시**  
3️⃣ **JDK Dynamic Proxy와 CGLIB**  
4️⃣ **스프링에서의 프록시 활용**  
5️⃣ **ProxyFactoryBean이란?**  

---

# **📌 1️⃣ 프록시란?**
✔ **프록시(Proxy)**: **대리인** 역할을 하는 객체  
✔ 클라이언트(사용자)는 프록시를 통해 타겟 객체(진짜 기능 수행하는 객체)를 호출  

📌 **실생활 예제: 집 계약**  
- 집을 구하는 사람이 **클라이언트**  
- 부동산 중개인이 **프록시**  
- 집주인이 **타겟 객체**  

💡 **왜 프록시를 사용할까?**  
✔ 집주인은 계약 업무에 신경 쓰지 않고 **자신의 일(집 관리)에만 집중**  
✔ 계약 업무는 중개인이(프록시) **대신 처리**  

---

# **📌 2️⃣ 정적 프록시 vs 동적 프록시**
## **✅ 1. 정적 프록시(Static Proxy)**
✔ 개발자가 **직접** 프록시 클래스를 만들어서 타겟을 감싸는 방식  

📌 **예제 코드 (Java)**
```java
interface Hello {
    String sayHello(String name);
}

class HelloTarget implements Hello {
    public String sayHello(String name) {
        return "Hello " + name;
    }
}

class HelloProxy implements Hello {
    private Hello target;

    public HelloProxy(Hello target) {
        this.target = target;
    }

    public String sayHello(String name) {
        return target.sayHello(name).toUpperCase(); // 대문자로 변환
    }
}

public class Main {
    public static void main(String[] args) {
        Hello hello = new HelloProxy(new HelloTarget());
        System.out.println(hello.sayHello("기론")); // "HELLO 기론"
    }
}
```
✔ **장점**: 코드가 직관적  
✔ **단점**: 프록시를 직접 구현해야 하므로 **중복 코드 발생, 복잡도 증가**  

---

## **✅ 2. 동적 프록시(Dynamic Proxy)**
✔ **프록시 클래스를 직접 만들지 않고, 런타임에 자동 생성**  
✔ 대표적인 방식: **JDK Dynamic Proxy, CGLIB**  

📌 **예제: 로봇 대여 서비스**  
- 클라이언트가 로봇을 빌리면, 프록시가 **대여 이력 기록** 후 로봇을 제공  
- 정적 프록시를 사용하면 모든 로봇마다 프록시 클래스를 만들어야 함  
- **동적 프록시를 사용하면 런타임에 자동으로 프록시를 생성**하여 해결  

---

# **📌 3️⃣ JDK Dynamic Proxy vs CGLIB**
✔ **JDK Dynamic Proxy**: 인터페이스 기반  
✔ **CGLIB**: 클래스 상속 기반  

---

## **✅ JDK Dynamic Proxy**
✔ **자바 기본 API 사용 → 별도 라이브러리 불필요**  
✔ **인터페이스 기반** (인터페이스 없으면 사용 불가)  

📌 **JDK Dynamic Proxy 코드 예제**
```java
import java.lang.reflect.InvocationHandler;
import java.lang.reflect.Method;
import java.lang.reflect.Proxy;

interface Service {
    void serve();
}

class RealService implements Service {
    public void serve() {
        System.out.println("서비스 실행!");
    }
}

class LoggingHandler implements InvocationHandler {
    private Object target;

    public LoggingHandler(Object target) {
        this.target = target;
    }

    public Object invoke(Object proxy, Method method, Object[] args) throws Throwable {
        System.out.println("로그: " + method.getName() + " 실행!");
        return method.invoke(target, args);
    }
}

public class Main {
    public static void main(String[] args) {
        Service service = (Service) Proxy.newProxyInstance(
            Service.class.getClassLoader(),
            new Class[]{Service.class},
            new LoggingHandler(new RealService())
        );
        service.serve();  // "로그: serve 실행!" → "서비스 실행!"
    }
}
```
✔ **장점**: 기본 제공 API 사용  
✔ **단점**: 인터페이스 필수, 리플렉션(Reflection) 사용으로 **성능 저하**  

---

## **✅ CGLIB**
✔ **클래스를 상속하여 프록시 생성** (인터페이스 없이도 가능)  
✔ **바이트코드 조작 → 성능 향상**  

📌 **CGLIB 코드 예제**
```java
import net.sf.cglib.proxy.Enhancer;
import net.sf.cglib.proxy.MethodInterceptor;
import net.sf.cglib.proxy.MethodProxy;
import java.lang.reflect.Method;

class ProductService {
    public void buy() {
        System.out.println("상품 구매!");
    }
}

class LoggingInterceptor implements MethodInterceptor {
    public Object intercept(Object obj, Method method, Object[] args, MethodProxy proxy) throws Throwable {
        System.out.println("로그: " + method.getName() + " 실행!");
        return proxy.invokeSuper(obj, args);
    }
}

public class Main {
    public static void main(String[] args) {
        ProductService productService = (ProductService) Enhancer.create(
            ProductService.class,
            new LoggingInterceptor()
        );
        productService.buy();  // "로그: buy 실행!" → "상품 구매!"
    }
}
```
✔ **장점**: 바이트코드 조작 → 성능 빠름  
✔ **단점**: **final 클래스/메서드는 프록시 적용 불가**  

---

# **📌 4️⃣ 스프링에서 프록시 활용**
✔ **스프링에서는 AOP(Aspect-Oriented Programming) 적용을 위해 프록시 사용**  
✔ 대표적인 예: `@Transactional` (트랜잭션 관리)  
✔ **스프링 부트 기본 설정**: CGLIB 사용  

📌 **스프링에서 트랜잭션 프록시 적용 예제**
```java
@Service
public class OrderService {
    @Transactional
    public void placeOrder() {
        System.out.println("주문 처리 중...");
    }
}
```
✔ `@Transactional`을 적용하면 **스프링이 자동으로 프록시 생성 → 트랜잭션 관리**  
✔ **인터페이스 기반이면 JDK Dynamic Proxy 사용, 클래스 기반이면 CGLIB 사용**  

---

# **📌 5️⃣ ProxyFactoryBean이란?**
✔ **프록시를 Spring Bean으로 등록하는 방법**  
✔ `ProxyFactoryBean`을 사용하면 **인터페이스 없이도 동작**  
✔ **MethodInterceptor 활용 → 독립적인 부가기능 유지 가능**  

📌 **ProxyFactoryBean 예제 (XML 기반)**
```xml
<bean id="orderService" class="org.springframework.aop.framework.ProxyFactoryBean">
    <property name="target" ref="realOrderService"/>
    <property name="interceptorNames">
        <list>
            <value>loggingInterceptor</value>
        </list>
    </property>
</bean>

<bean id="loggingInterceptor" class="com.example.LoggingInterceptor"/>
<bean id="realOrderService" class="com.example.OrderService"/>
```
✔ 프록시를 **스프링 빈(Bean)으로 등록하여 관리 가능**  
✔ **타겟 객체를 직접 참조하지 않음 → 부가기능을 싱글톤으로 유지 가능**  

---

# **📌 결론**
📢 **"프록시는 객체를 감싸서 부가기능을 추가하는 역할!"**  
✔ **JDK Dynamic Proxy**: 인터페이스 기반, 리플렉션 사용  
✔ **CGLIB**: 클래스 기반, 바이트코드 조작으로 성능 빠름  
✔ **스프링에서는 트랜잭션, AOP 적용 시 프록시 활용**  
✔ **ProxyFactoryBean을 사용하면 프록시를 빈으로 쉽게 관리 가능**  

🚀 **"무작정 기술을 적용하지 말고, 언제 어떤 방식이 필요한지 이해하고 사용하자!"**

