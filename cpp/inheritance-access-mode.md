# Inheritance access mode

C++에서의 클래스 상속은 아래와 같이 선언할 수 있다.

```jsx
class Base {} // 기반 클래스

class Derived : public Base {} // 파생 클래스
```

Derived 클래스에서 콜론으로 구분된 Base 클래스를 상속받는 것은 이해할 수 있지만, 중간에 포함된 `public` 은 무슨 뜻일까?

우선 위 코드에서 `public` 을 지칭하는 용어는 접근 지정자이다.

일반적으로 클래스를 만들 때, 내부 변수와 함수들을 각 특성에 맞게 접근 정도를 지정해주는데 `public`, `protected`, `private` 으로 나뉜다.

각 접근 지정자는 아래와 같은 권한을 가진다.

`public` : 어디서든 접근 가능

`private` : 기반(base) 클래스에서만 접근 가능

`protected` : 기반(base) 클래스, 파생(derived) 클래스에서 접근 가능

위와 같이 파생 클래스에서 상속을 받는 클래스의 요소들에 대해 접근 지정자를 설정할 수 있는데, 각 지정자는 아래와 같은 역할을 한다.

`public` : 기반 클래스 요소들의 접근 지정자를 그대로 두고 상속한다.(public은 public, protected는 protected)

`private` : 기반 클래스 요소들의 접근 지정자를 모두 private으로 상속한다.

`protected` : 기반 클래스 요소들의 접근 지정자를 모두 protected으로 상속한다.

(`private` 접근 지정자인 요소들은 파생 클래스에서 접근 불가한 요소이기 때문에, 고려하지 않는다.)

### Reference

[C++ Public, Protected and Private Inheritance](https://www.programiz.com/cpp-programming/public-protected-private-inheritance)