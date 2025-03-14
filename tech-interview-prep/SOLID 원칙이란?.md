## SOLID 원칙
- SOLID 원칙은 객체지향 설계 5원칙이라고도 불리며, 각 원칙의 앞 글자를 따서 만들어졌습니다.
- 객체지향설계의 핵심 중 하나는 의존성을 관리하는 것인데요. 의존성을 잘 관리하기 위해서는 SOLID 원칙을 준수해야 합니다.

<br>

---

<br>

## 단일 책임 원칙(Single Responsibilty Principle) 
- 단일 책임 원칙(Single Responsibilty Principle) 은 클래스가 오직 하나의 목적이나 이유로만 변경되어야 한다는 것을 강조합니다.
- 여기서 “책임”이란 단순히 메서드의 개수를 뜻하지 않고, 특정 사용자나 기능 요구사항에 따라 소프트웨어의 변경 요청을 처리하는 역할을 의미합니다.
- 즉, 클래스는 한 가지 변화의 이유만 가져야 하며, 이를 통해 변경이 발생했을 때 다른 기능에 영향을 덜 미치도록 설계됩니다.
- 이렇게 하면 유지보수가 쉬워지고 코드가 더 이해하기 쉬워집니다.

<br>

---


## 개방 폐쇄 원칙(Open-Closed Principle) 
- 개방 폐쇄 원칙(Open-Closed Principle) 은 확장에는 열려있고, 변경에는 닫혀 있어야 함을 강조합니다.
- 이때 확장이란 새로운 타입을 추가함으로써 새로운 기능을 추가하는 것을 의미하며, 폐쇄란 확장이 일어날 때 상위 레벨의 모듈이 영향을 받지 않아야 함을 의미합니다.
- 이를 통해서 모듈의 행동을 쉽게 변경할 수 있습니다.
- 모듈이란 크기와 상관없이 클래스, 패키지, 라이브러리와 같이 프로그램을 구성하는 임의의 요소를 의미합니다.


<br>

---


## 리스코브 치환 원칙(Liskov Substitution Principle)
- 리스코브 치환 원칙(Liskov Substitution Principle)은 서브 타입은 언제나 상위 타입으로 교체할 수 있어야 합니다.
- 즉, 서브 타입은 상위 타입이 약속한 규약을 지켜야 함을 강조합니다. 이 원칙은 부모 쪽으로 업 캐스팅하는 것이 안전함을 보장하기 위해 존재합니다.
- 상위 타입에 대해 기대되는 역할과 행동 규약이 있는데 이를 벗어나면 안 됩니다.
- 만약, 하위 타입이 상위 타입에 기대되는 역할을 만족하지 않는다면, 상위 타입을 사용하는 클라이언트 코드에서는 하위 타입이 누구인지 물어봐야 하는데, 이는 OCP를 달성하기 어렵게 합니다.
- LSP를 위반하는 대표적인 사례로는 Rectangle 예제가 있습니다.


<br>

---

## 인터페이스 분리 원칙(Interface Segregation Principle)
- 인터페이스 분리 원칙(Interface Segregation Principle) 은 클라이언트 입장에서 인터페이스를 분리해야 함을 강조합니다.
- 사용하지 않지만 의존성을 가지고 있다면 해당 인터페이스가 변경되는 경우 영향을 받습니다. 따라서, 독립적인 개발과 배포가 불가합니다.
- 사용하는 기능만 제공하도록 인터페이스를 분리해 변경의 여파를 최소화할 수 있습니다.

<br>

---

## 의존성 역전 원칙(Dependency Inversion Principle)
- 의존성 역전 원칙(Dependency Inversion Principle) 은 상위 수준의 모듈은 하위 수준의 모듈에 의존해서는 안 되며, 모두 추상화에 의존해야 함을 강조합니다.
- SOLID는 서로 연관이 있는데요. 의존성 역전 원칙을 통해서 하위 레벨의 모듈은 개방 폐쇄 원칙을 준수하면서 새로운 타입이 추가 가능합니다.


---

<br>
<br>

## 앞으로 어떤 확장이 필요한지 완벽히 알아야 OCP를 제대로 할 수 있는 거 아닌가요?
- 변경을 예상하고, 준비하지 말고 고객이 원한 것만 만들어서 빨리 전달하고 피드백을 수용하는 방법을 사용해 볼 수 있습니다.
- 변화에 대한 가장 좋은 예측은 변화를 경험하는 것이라고 생각합니다. 발생할 것 같은 변화를 발견한다면 향후 해당 변화와 같은 종류의 변화로부터 코드를 보호할 수 있습니다.
- 즉, 고객이 요구할 모든 종류의 변경을 완벽하게 예측하고, 이에 대한 변경에 대응하기 위해 추상화를 적용하는 대신에 고객이 변경을 요구할 때까지 기다리고 추상화를 만들어서 향후 추가로 재발하는 변화로부터 보호될 수 있도록 하는 것입니다.
- 이때 OCP를 준수하도록 코드를 작성할 수 있습니다.

<br>


---
---

<br><br>

> ## 추가학습자료

[10분 테코톡] 클로버의 SOLID
출처 : https://www.youtube.com/watch?v=7c0tqHLfxlE

<Br>

# 🚀 SOLID 원칙 정리 & 쉽게 이해하는 비유

SOLID 원칙에 대해 **쉽고 직관적으로 이해할 수 있도록** 구성했습니다.  
각 원칙을 **누락 없이 깔끔하게 정리**하고, **일상적인 비유**를 들어 개념을 명확하게 전달하겠습니다.  

---

## **SOLID 원칙이란?**
SOLID 원칙은 객체지향 프로그래밍에서 **유지보수성과 확장성을 높이기 위해** 고안된 **5가지 원칙**입니다.  
이 원칙들은 코드가 **더 유연하고, 재사용 가능하며, 변경에 강한 구조를 갖도록 도와줍니다.**  
각 원칙은 **객체의 역할, 확장성, 상속 관계, 인터페이스 설계, 의존성 관리**에 대한 지침을 제공합니다.

<br>

---

## **1️⃣ 단일 책임 원칙 (Single Responsibility Principle, SRP)**  
> 📌 **"객체는 단 하나의 책임만 가져야 한다."**  
> 📌 **"변경의 이유는 단 하나여야 한다."**

<br>

### **📍 쉽게 이해하는 비유**
**👨‍🍳 요리사에게 서빙을 시키지 마세요!**  
한 식당에서 **요리사**가 음식을 만들고, 서빙까지 한다면 어떤 일이 생길까요?  
- 요리를 하다가 손님이 오면 서빙하러 가야 한다.  
- 요리를 하는 도중 주문이 밀리면 서빙도 늦어진다.  
- 만약 **요리를 변경해야 한다면(새로운 레시피 추가)**, **서빙 방식도 바뀌어야 할 수도 있다.**  

**💡 해결책:**  
요리사는 요리만! 서빙 담당은 서빙만!  
이처럼 **하나의 역할만 담당하도록 나누면, 각각의 역할이 독립적으로 유지**될 수 있습니다.

<br>

### **📍 코드 예제**
```java
// ❌ 단일 책임 원칙을 위반한 코드
class ReportGenerator {
    public void generateReport() {
        // 리포트 생성 로직
    }

    public void saveToDatabase() {
        // 데이터베이스 저장 로직
    }
}
```
위 코드는 **"리포트 생성"**과 **"데이터 저장"**이라는 **두 개의 책임**을 가지고 있습니다.

✅ **단일 책임 원칙을 적용한 코드**
```java
class ReportGenerator {
    public void generateReport() {
        // 리포트 생성 로직
    }
}

class ReportSaver {
    public void saveToDatabase() {
        // 데이터베이스 저장 로직
    }
}
```
**역할을 분리하여, 변경이 필요할 때 영향이 최소화됩니다!**

---

## **2️⃣ 개방-폐쇄 원칙 (Open-Closed Principle, OCP)**  
> 📌 **"확장에는 열려 있고, 변경에는 닫혀 있어야 한다."**  
> 📌 **"새로운 기능을 추가할 때 기존 코드를 수정하지 않도록 설계해야 한다."**

<br>

### **📍 쉽게 이해하는 비유**
**📺 TV를 바꾸지 말고 리모컨을 바꾸세요!**  
TV를 조작하는 방법이 바뀌었을 때,  
- 기존 TV를 다 분해해서 버튼을 바꿔야 할까요? ❌  
- 리모컨의 버튼만 변경하면 될까요? ✅  

**💡 해결책:**  
TV의 **기본 기능(추상화된 인터페이스)**을 유지한 채,  
리모컨(구현체)만 교체하면 쉽게 확장할 수 있습니다.  

<br>

### **📍 코드 예제**
```java
// ❌ 개방-폐쇄 원칙을 위반한 코드
class NotificationService {
    public void sendEmail() {
        System.out.println("Sending Email...");
    }

    public void sendSMS() {
        System.out.println("Sending SMS...");
    }
}
```
만약 **새로운 알림 방식 (예: 카카오톡 알림)**을 추가하려면?  
→ 기존 `NotificationService`를 수정해야 합니다. (OCP 위반)

✅ **OCP를 적용한 코드**
```java
interface Notification {
    void send();
}

class EmailNotification implements Notification {
    public void send() {
        System.out.println("Sending Email...");
    }
}

class SMSNotification implements Notification {
    public void send() {
        System.out.println("Sending SMS...");
    }
}

class NotificationService {
    public void sendNotification(Notification notification) {
        notification.send();
    }
}
```
💡 **새로운 알림 방식을 추가하려면?**  
→ `Notification` 인터페이스를 구현한 새로운 클래스를 추가하면 끝!  
(기존 `NotificationService` 코드는 수정할 필요 없음)

---

## **3️⃣ 리스코프 치환 원칙 (Liskov Substitution Principle, LSP)**  
> 📌 **"자식 클래스는 부모 클래스를 대체할 수 있어야 한다."**  
> 📌 **"부모 클래스를 사용하는 코드에서, 자식 클래스로 대체해도 정상적으로 동작해야 한다."**

<br>

### **📍 쉽게 이해하는 비유**
**🖥️ 모니터를 바꾸는 건 쉬워야 한다.**  
모니터를 교체할 때,  
- 삼성 모니터를 LG 모니터로 바꿔도 **PC가 정상적으로 작동해야 한다.**  
- 만약 LG 모니터는 특정한 방식으로만 연결해야 한다면? → 문제가 발생!  

**💡 해결책:**  
모든 모니터가 **동일한 인터페이스(HDMI, DisplayPort 등)**를 따르도록 하면,  
브랜드가 달라도 자유롭게 교체할 수 있습니다.

<br>

### **📍 코드 예제**
```java
// ❌ LSP 위반 예제
class Rectangle {
    protected int width;
    protected int height;

    public void setWidth(int width) { this.width = width; }
    public void setHeight(int height) { this.height = height; }
}

class Square extends Rectangle {
    @Override
    public void setWidth(int width) {
        this.width = width;
        this.height = width;  // ❌ 정사각형은 너비를 바꾸면 높이도 같이 변경됨
    }

    @Override
    public void setHeight(int height) {
        this.width = height;
        this.height = height;
    }
}
```
💡 **문제점:**  
기존 `Rectangle`을 사용하는 코드는 `Square`로 대체되었을 때 예상과 다르게 동작할 수 있습니다.  

✅ **LSP를 만족하도록 개선**
```java
interface Shape {
    int getArea();
}

class Rectangle implements Shape {
    protected int width;
    protected int height;
    
    public void setWidth(int width) { this.width = width; }
    public void setHeight(int height) { this.height = height; }
    
    public int getArea() { return width * height; }
}

class Square implements Shape {
    protected int side;
    
    public void setSide(int side) { this.side = side; }
    
    public int getArea() { return side * side; }
}
```
`Rectangle`과 `Square`를 분리하여, 서로 다른 방식으로 동작하도록 했습니다.  
이제 **부모 클래스를 대체해도 예상한 대로 동작합니다!**

---

# **📌 마무리 정리**
| 원칙 | 설명 | 위반 시 문제 | 해결 방법 |
|------|------|------|------|
| **SRP** (단일 책임) | 객체는 하나의 역할만 담당해야 함 | 유지보수 어려움 | 역할을 분리하여 독립성 유지 |
| **OCP** (개방-폐쇄) | 확장에 열려 있고, 변경에는 닫혀 있어야 함 | 새로운 기능 추가 시 기존 코드 수정 필요 | 인터페이스 활용하여 변경 없이 확장 가능 |
| **LSP** (리스코프 치환) | 자식 클래스는 부모 클래스를 대체할 수 있어야 함 | 예상과 다르게 동작 | 하위 클래스가 상위 클래스의 동작을 유지하도록 설계 |

---

🚀 **이제 SOLID 원칙을 더 명확하게 이해할 수 있겠죠?**  
코드 설계를 할 때, **이 원칙들을 항상 떠올리면서 구조를 고민해보세요!** 💡
