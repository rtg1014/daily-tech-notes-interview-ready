## GC(Garbage Collection)
- GC(Garbage Collection)는 자바의 메모리 관리 방법의 하나이며, JVM의 힙 영역에서 동적으로 할당했던 메모리 중에서 필요 없어진 객체를 주기적으로 제거하는 것을 의미합니다.
- GC는 특정 객체가 사용 중인지 아닌지 판단하기 위해서 도달 가능성(Reachability) 라는 개념을 사용하는데요.
- 특정 객체에 대한 참조가 존재하면 도달할 수 있으며, 참조가 존재하지 않는 경우에 도달할 수 없는 상태로 간주합니다.
- 이때, 도달할 수 없다는 결론을 내린다면 해당 객체는 GC의 대상이 됩니다.

<br>

---

<br>


## 도달 가능성은 어떻게 판단하나요? 
- 힙 영역에 있는 객체에 대한 참조는 4가지 케이스가 존재하는데요.
- 힙 내부 객체 간의 참조, 스택 영역의 변수에 의한 참조, JNI에 의해 생성된 객체에 대한 참조(네이티브 스택 영역), 메서드 영역의 정적 변수에 의한 참조가 이에 해당됩니다.
- 이때, 힙 내부 객체 간의 참조를 제외한 나머지를 Root Set이라고 합니다.
- Root Set으로부터 시작한 참조 사슬에 속한 객체들은 도달할 수 있는 객체이며, 이 참조 사슬과 무관한 객체들은 도달하기 어렵기 때문에 GC에 대상이 됩니다.

  
<br>

---

<br>

개발자가 GC 대상 판단에 관여할 수는 없나요? 

```java
Origin o = new Origin();
WeakReference<Origin> wo = new WeakReference<>(o);
```

- 자바에서는 java.lang.ref 패키지의 SoftReference, WeakReference 클래스를 통해 개발자가 GC 대상 판단에 일정 부분 관여할 수 있습니다.
- 해당 클래스들의 객체(reference object)는 원본 객체(referent)를 감싸서 생성하는데요. 이렇게 생성된 객체는 GC가 특별하게 취급합니다.
- SoftReference 객체에 감싸인 객체는 Root Set으로부터 참조가 없는 경우에, 남아있는 힙 메모리의 크기에 따라서 GC 여부가 결정됩니다.
- 반면, WeakReference 객체에 감싸인 객체는 Root Set으로부터 참조가 없는 경우, 바로 GC 대상이 됩니다.



---
---

> ## 추가 학습자료 정리


## Garbage Collection(가비지 컬렉션)
- 프로그램을 개발하다 보면 유효하지 않은 메모리인 가비지(Garbage)가 발생하게 된다.
- C언어를 이용하면 free()라는 함수를 통해 직접 메모리를 해제해주어야 하지만 Java나 JavaScript을 이용해 개발을 하다보면 개발자가 메모리를 직접 해제해주는 일은 없다.
- 그 이유는 JVM의 Garbage Collector가 프로그램이 동적으로 할당했던 메모리 영역 중 불필요한 메모리를 알아서 정리(해제)해주기 때문이다.
- 여기서 동적으로 할당했던 메모리 영역은 프로그램 런타임에 사용되는 Heap 메모리 영역을 뜻하고, 불필요한 영역은 어떤 변수도 가리키지 않게 된 영역을 의미한다.

 

### 장점
이렇게 GC를 도입하면 수동으로 메모리를 관리하던 것에서 비롯된 에러들을 방지할 수 있다.

- 개발자의 실수로 인한 메모리 누수 방지
- 해제된 메모리에 접근하는 오류 방지
- 해제된 메모리를 또 해제하는 이중 해제 방지

 <Br>

### 단점
- 어떠한 메모리 영역이 해제의 대상이 될지 검사하고 해제하는 일은 프로그램이 해야하는 일을 못하도록 방해하는 오버헤드
- GC의 메모리 해제 타이밍을 개발자가 정확하게 알기 어렵다.
- 이런 특성에 따라 실시간성이 매우 강조되는 프로그램의 경우 GC에게 메모리 관리를 맡기는 것이 알맞지 않을 수 있다.

 

## GC 알고리즘
- 그렇다면 GC는 어떻게 해제할 동적 메모리 영역들을 알아서 판단할까?

---


## **📌 JVM에서 GC 대상 객체를 판단하는 기준**
JVM(Java Virtual Machine)에서 **GC(Garbage Collection, 가비지 컬렉션)**이 수행될 때,  
**어떤 객체를 제거할지 판단하는 기준**을 이해하는 것이 중요합니다.

---

## **✅ 1. GC 대상 객체를 판단하는 기준**
JVM은 **"더 이상 사용되지 않는 객체"**를 자동으로 제거합니다.  
객체가 **GC의 대상이 되는지 판단하는 방법**은 다음과 같습니다.

### **📌 1️⃣ 참조 객체(Graph Reachability) 방식 (Reachability Analysis)**
- **JVM은 "객체가 사용되고 있는지"를 판단하기 위해 "객체 그래프 탐색"을 수행합니다.**
- **"GC Root"**에서 시작하여 **도달할 수 없는(Unreachable) 객체를 GC 대상으로 간주**합니다.

✅ **GC Root가 될 수 있는 대상 (즉, 삭제되지 않는 객체)**
1. **JVM 스택(Stack)에 있는 지역 변수** (메서드 실행 중에 사용되는 변수)
2. **메서드 영역(Method Area)에 있는 클래스(static 변수)**
3. **JNI (Native 코드에서 참조하는 객체)**
4. **쓰레드(Thread) 객체** (현재 실행 중인 쓰레드)

✔ **GC 대상이 되는 경우**:
- 위의 GC Root에서 **연결이 끊어진(Unreachable) 객체**는 **GC의 대상**이 됩니다.

---

### **📌 2️⃣ 객체의 생존 여부 확인 방법**
JVM은 특정 객체가 **GC 대상인지 확인하는 두 가지 방식**을 사용합니다.

#### **✔ 1. 참조 카운팅(Reference Counting) - 사용 안 함**
- 객체가 참조될 때마다 **참조 카운터**를 증가, 참조가 사라지면 감소하는 방식.
- **문제점**: 서로가 서로를 참조하는 **순환 참조(Circular Reference) 문제**를 해결하지 못함.

✅ **예제 (순환 참조 문제 발생)**  
```java
class Node {
    Node next;
}
public class Test {
    public static void main(String[] args) {
        Node a = new Node();
        Node b = new Node();
        
        a.next = b;
        b.next = a;  // 서로를 참조함 (순환 참조 발생)
        
        a = null;
        b = null;  // 모든 변수를 null로 설정해도 GC 대상이 아님!
    }
}
```
✔ **해결 방법** → **현재 JVM에서는 참조 카운팅 방식이 아닌 "Reachability Analysis"를 사용!**

---

#### **✔ 2. 도달 가능성 분석(Reachability Analysis) - 사용 중**
- GC Root에서 **연결이 끊어진(Unreachable) 객체를 GC 대상으로 판단**하는 방식.
- **현재 대부분의 JVM에서 사용되는 방식**입니다.

✅ **예제 (GC Root에서 도달 가능한지 확인)**
```java
public class TestGC {
    static Object globalObj; // static 변수 (GC Root)

    public static void main(String[] args) {
        Object localObj = new Object(); // 스택 변수 (GC Root)

        globalObj = new Object(); // static 변수로 참조되므로 GC 대상 아님

        localObj = null; // localObj는 이제 GC 대상!
    }
}
```
✔ **`globalObj`는 여전히 `static`으로 참조되므로 GC 대상이 아니지만, `localObj`는 GC 대상이 됨.**

---

### **📌 3️⃣ finalize() 메서드 실행 여부**
- **객체가 GC 대상이 되기 전에 `finalize()` 메서드가 실행될 수도 있음**.
- 하지만, **한 번만 실행되며, JVM이 보장하지 않으므로 신뢰하면 안 됨**.
  
✅ **예제 (`finalize()` 메서드 활용)**
```java
class TestFinalize {
    @Override
    protected void finalize() throws Throwable {
        System.out.println("GC가 객체를 수거하기 전에 finalize() 실행!");
    }
}

public class Main {
    public static void main(String[] args) {
        TestFinalize obj = new TestFinalize();
        obj = null; // 참조 해제 → GC 대상

        System.gc(); // 강제 GC 요청
    }
}
```
✔ **결과**: `"GC가 객체를 수거하기 전에 finalize() 실행!"`  
✔ 하지만, **`finalize()` 실행을 보장할 수 없으므로 사용을 권장하지 않음**.

---

## **✅ 2. GC에서 핵심적으로 알아야 하는 개념**
JVM의 GC를 이해하기 위해 **필수적인 개념**을 정리하겠습니다.

### **📌 1️⃣ Stop-the-world (STW)**
- GC가 실행될 때 **애플리케이션의 모든 실행을 멈추고 GC를 수행하는 과정**입니다.
- **STW 시간이 길어지면 애플리케이션이 멈춘 것처럼 보일 수 있음**.

✅ **해결 방법**  
- 최신 GC 알고리즘에서는 **STW 시간을 최소화하기 위해 병렬(Parallel), 동시(Concurrent) GC 방식**을 사용.

---

### **📌 2️⃣ JVM의 힙 메모리 구조**
JVM의 힙 메모리는 **세대(Generation)별로 구분**되어 있으며,  
**GC는 각 세대별로 다르게 동작**합니다.

| 세대 | 특징 | GC 발생 시점 |
|------|------|--------------|
| **Young Generation** | 새롭게 생성된 객체가 저장됨 | Minor GC 발생 |
| **Old Generation** | 오래된 객체가 저장됨 | Major GC (Full GC) 발생 |
| **Metaspace (PermGen 대체)** | 클래스 메타정보 저장 | GC 대상 아님 |

---

### **📌 3️⃣ GC의 종류**
JVM에서 사용하는 대표적인 GC 알고리즘은 다음과 같습니다.

| GC 알고리즘 | 특징 | 장점 | 단점 |
|------------|------|------|------|
| **Serial GC** | 단일 스레드 GC | 간단, 메모리 사용 적음 | STW 시간이 김 |
| **Parallel GC** | 다중 스레드 사용 | STW 감소 | CPU 사용량 증가 |
| **CMS GC** | 애플리케이션과 병렬 실행 | STW 최소화 | CPU 부하 높음 |
| **G1 GC** | Young/Old를 동시에 처리 | 예측 가능한 STW | 설정 복잡 |

✔ **최근 JVM에서는 G1 GC가 기본으로 사용됨** (`Java 9 이상`).  

✅ **G1 GC 설정 예제**
```java
java -XX:+UseG1GC -Xms512m -Xmx2g MainClass
```
✔ `-XX:+UseG1GC` → G1 GC 활성화  
✔ `-Xms512m` → 최소 힙 크기 설정  
✔ `-Xmx2g` → 최대 힙 크기 설정  

---

## **✅ 3. GC 대상 객체를 쉽게 이해하는 예시**
💡 **도서관에서 책을 빌리는 개념으로 GC를 이해해 보겠습니다!** 📚

### **📌 예제: 도서관 책 관리와 GC**
1. **책을 대출(객체 생성)** → 도서관에 새로운 책(객체)이 들어옴.
2. **책을 반납(참조 해제)** → 더 이상 필요하지 않은 책이 있음.
3. **대출 중인 책(GC Root와 연결됨)** → GC 대상이 아님.
4. **고객이 반납한 책(연결 끊김)** → GC가 수거하여 제거.

```java
public class LibraryGC {
    static Book borrowedBook; // static 변수 (GC 대상 아님)

    public static void main(String[] args) {
        Book myBook = new Book("자바의 정석"); // 대출 (객체 생성)

        borrowedBook = new Book("이펙티브 자바"); // GC 대상 아님 (static 변수)
        myBook = null; // 책 반납 (GC 대상)

        System.gc(); // GC 요청
    }
}
```
✔ **대출 중인 책(`borrowedBook`)은 GC 대상이 아니지만, `myBook`은 더 이상 참조되지 않으므로 GC 대상이 됩니다!**  

---

## **✅ 4. 결론**
💡 **JVM에서 GC 대상 객체는 다음과 같은 기준으로 판단됩니다.**
1️⃣ **GC Root에서 접근할 수 없는 객체는 GC의 대상이 된다.**  
2️⃣ **Reachability Analysis (객체 도달 가능성 분석)가 GC 대상 여부를 판단한다.**  
3️⃣ **힙 메모리는 Young, Old 세대로 나뉘며, GC는 세대별로 다르게 동작한다.**  
4️⃣ **GC는 Stop-the-World(STW) 시간 단축을 위해 병렬/동시 GC 기법을 활용한다.**  
5️⃣ **JVM의 최신 GC(G1 GC 등)를 활용하면 GC 성능을 최적화할 수 있다.**  

🚀 **즉, 참조가 끊어진 객체는 GC의 대상이 되며, GC 알고리즘은 성능 최적화를 위해 발전해 왔습니다!** 🚀


