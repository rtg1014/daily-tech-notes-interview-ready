
## 결론
- String 객체는 불변(Immutable) 입니다. String 클래스는 내부적으로 final 키워드가 선언된 byte[] 필드를 사용해서 문자열을 저장하기 때문입니다.
- 또한, String은 참조 타입(Reference Type)이기 때문에 concat(), replace(), toUpperCase()와 같은 String 메서드를 호출하면 새로운 String 객체를 참조하고 기존 객체를 수정하지 않습니다. 따라서 String 객체를 불변하게 유지할 수 있습니다.

<br><br>



## String을 불변으로 설계한 이유는 무엇일까요?
String을 불변으로 설계한 덕분에 많은 이점을 얻을 수 있습니다.

- String Constant Pool을 사용할 수 있습니다. 이를 통해 동일한 문자열의 String 변수들은 같은 객체를 공유하기 때문에 메모리를 효율적으로 사용할 수 있습니다.
- 불변한 객체는 멀티 스레드 환경에서 thread-safe합니다. 문자열을 변경하면 String Constant Pool에 새로운 객체를 생성하기 때문에 동기화를 신경쓸 필요가 없습니다.
- 해시코드를 한 번만 계산하고 이를 캐싱해서 재사용할 수 있습니다.
- 비밀번호, 토큰, URL 등의 민감한 정보를 안전하게 다룰 수 있습니다. 불변한 객체는 변경할 수 없기 때문에 민감한 정보가 예기치 않게 수정되는 것을 방지할 수 있습니다.


## 리터럴로 생성한 String 객체와 생성자로 생성한 String 객체를 비교하면 어떤 차이가 있을까요?
- 두 방식으로 생성한 객체는 같은 문자열을 갖더라도 메모리 상에서 다르게 처리됩니다.

```java
String first = "hello"; // 리터럴로 생성
String second = new String("hello"); // 생성자로 생성
String third = "hello";

System.out.println(System.identityHashCode(first)); // 498931366
System.out.println(System.identityHashCode(second)); // 2060468723
System.out.println(System.identityHashCode(third)); // 498931366
```


<br><br>

리터럴로 생성한 String 객체는 Heap 영역의 String Constant Pool에 저장되어 동일한 문자열을 재사용할 수 있습니다. 문자열이 String Constant Pool에 이미 존재하면 같은 주소를 참조합니다. 반면, 생성자로 생성한 String 객체는 Heap 영역에 저장되어 동일한 문자열이더라도 항상 새로운 객체를 생성합니다.

```java
tring first = "hello";
String second = new String("hello");
String third = second.intern(); // intern() 메서드 사용

System.out.println(System.identityHashCode(first)); // 498931366
System.out.println(System.identityHashCode(second)); // 2060468723
System.out.println(System.identityHashCode(third)); // 498931366
```

<br>

intern() 메서드를 사용하면 Heap 영역에 저장된 String 객체를 String Constant Pool에 저장할 수 있습니다. intern() 메서드는 해당 문자열이 String Constant Pool에 존재할 경우 그 주솟값을 반환하고, 없을 경우 String Constant Pool에 추가하고 새로운 주솟값을 반환합니다.

---

<br><br>


> ## 추가 학습 및 기술면접 대비자료


---

## 📌 1. 질문:  
### "문자열을 반복적으로 조작할 때 어떤 클래스를 사용할 건가요?"

✅ **답변**:  
> 문자열을 반복적으로 조작해야 한다면, `StringBuilder`를 사용하겠습니다.  
> `String`은 불변 객체이기 때문에 문자열을 변경할 때마다 새로운 객체가 생성되어 메모리 낭비가 크고 성능도 떨어질 수 있습니다.  
> `StringBuilder`는 내부적으로 가변적인 `char[]` 배열을 사용해 성능이 훨씬 좋습니다.  
> 만약 멀티스레드 환경에서 동기화가 필요하다면 `StringBuffer`를 사용하겠습니다.

💡 **비유**:  
- `String`은 매번 새 종이에 다시 쓰는 것과 같고,  
- `StringBuilder`는 같은 칠판에 계속 덧칠하면서 쓰는 것과 같아요.  
- `StringBuffer`는 줄 서서 칠판에 한 명씩 쓰는 구조(스레드 안전)입니다.

---

## 📌 2. 질문:  
### "StringBuffer와 StringBuilder의 차이점은?"

✅ **답변**:  
> `StringBuffer`와 `StringBuilder` 모두 가변 객체이며, 문자열을 효율적으로 조작할 수 있습니다.  
> 가장 큰 차이는 **스레드 안전성**입니다.  
> `StringBuffer`는 모든 메서드가 `synchronized`로 감싸져 있어서 **멀티스레드 환경**에서도 안전하지만,  
> `StringBuilder`는 동기화를 제공하지 않기 때문에 **단일 스레드 환경에서 빠릅니다**.

💡 **비유**:  
- `StringBuffer`는 혼잡한 식당에서 한 명씩 줄 서서 주문하는 느낌  
- `StringBuilder`는 혼자 있는 집에서 자유롭게 요리하는 느낌

---

## 📌 3. 질문:  
### "String에서 ==과 equals의 차이는?"

✅ **답변**:  
> `==`은 **주소값(참조)** 비교이고,  
> `equals()`는 **내용(값)** 비교입니다.  

예제 코드:
```java
String a = "hello";
String b = "hello";
String c = new String("hello");

System.out.println(a == b); // true (리터럴이기 때문에 같은 객체)
System.out.println(a == c); // false (new로 새로운 객체 생성됨)
System.out.println(a.equals(c)); // true (값은 같음)
```

💡 **비유**:  
- `==`은 "두 사람이 같은 집에 사는가?"  
- `equals()`는 "두 사람이 이름이 같은가?"

---

## 📌 4. 질문:  
### "HashMap의 key로 String을 사용할 때 equals와 hashCode가 왜 중요한가요?"

✅ **답변**:  
> `HashMap`은 내부적으로 **hashCode()를 먼저 비교**해서 같은 해시 버킷에 있는지를 확인하고,  
> 그 다음 **equals()를 사용해서 진짜 같은 값인지 확인**합니다.  
> 그래서 `String`을 key로 사용할 때는 **hashCode()와 equals()가 일관되게 동작하는 것이 매우 중요**합니다.

예시:
```java
Map<String, String> map = new HashMap<>();
map.put("abc", "value");

System.out.println(map.get(new String("abc"))); // "value"
```

- 여기서 `"abc"`와 `new String("abc")`는 주소는 다르지만 값과 hashCode가 같기 때문에 정상 작동함

💡 **비유**:  
- `hashCode()`는 사람 이름 앞글자,  
- `equals()`는 실제 전체 이름을 확인하는 것  
→ 앞글자가 같아야 그 그룹에 들어가고, 이름이 완전히 같아야 해당 사람을 찾음

---

## 📌 5. 실습 코드 예시 관련 설명

### "왜 `+` 연산으로 문자열을 붙이면 성능이 떨어질까요?"

✅ **답변**:  
> 자바에서 `+` 연산을 사용하면 내부적으로 `StringBuilder`를 만들어서 append 연산을 수행한 후 `toString()`으로 변환합니다.  
> 하지만 루프에서 매번 `+` 연산을 쓰면 매 반복마다 새로운 `StringBuilder` 객체가 생성되므로 비효율적입니다.

비효율적 예:
```java
String s = "";
for (int i = 0; i < 1000; i++) {
    s += i; // 매번 새로운 StringBuilder 생성 → 성능 저하
}
```

효율적 예:
```java
StringBuilder sb = new StringBuilder();
for (int i = 0; i < 1000; i++) {
    sb.append(i);
}
String s = sb.toString(); // 최종 문자열
```

💡 **요약**:  
> 반복적인 문자열 조작 → `StringBuilder`  
> 멀티스레드 → `StringBuffer`  
> 값 변경 없는 읽기 위주 → `String`

---

## 🔁 마무리 팁: "외워두면 좋은 구분 키워드"

| 항목                 | 불변성 | 스레드 안전 | 성능     | 메모리 효율 |
|----------------------|--------|-------------|----------|-------------|
| String               | ✅     | ✅          | ❌       | ✅          |
| StringBuilder        | ❌     | ❌          | ✅✅✅    | ❌          |
| StringBuffer         | ❌     | ✅          | ✅       | ❌          |

---

