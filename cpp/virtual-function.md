# Virtual function

## Virtual function

C++과 같은 객체 지향 언어의 다형성에서 중요한 부분으로 가상 함수(virtual function)는 동적 디스패치(dynamic dispatch)를 가능하게 하는 상속과 오버라이딩을 할 수 있게 하는 함수다.

짧게 말하면, 컴파일 타임에 실행할 함수를 알지 못해도, 가상 함수가 실행될 수 있도록 정의해준다.

많은 언어(Javascript, PHP, Python 등)에서 기본적으로 모든 함수를 가상 함수로 취급하고, 이를 강제한다.
하지만, Java와 PHP에서는 파생 클래스에서 상속 받지 않도록 변경해줄 수 있다.

객체 지향 프로그래밍에서 파생 클래스는 포인터 또는 참조자를 통해 기반 클래스 타입을 사용할 수 있는데, 파생 클래스에 오버라이딩된 함수가 있으면 `일찍`(컴파일러에 의해 기반 클래스의 함수가) 바인드(링크)될 수도 있고, `늦게`(런타임에 파생 클래스의 함수가) 바인드될 수도 있다.

가상 함수는 위에서 명시한 방식 중, `늦게` 바인드되게 한다.

C++에서, 가상 함수는 기반 클래스의 함수 앞에 `virtual` 키워드를 붙이는 방식으로 사용할 수 있으며, 가상 함수로 만들게 되면 파생 클래스에서 동일한 함수명을 가진 모든 함수에 적용된다.

이는 지속적으로 오버 라이딩이 가능하며, 늦은 바인딩을 지원한다.

## Virtual table

클래스가 가상 함수를 가지고 있거나, 부모 클래스의 가상 함수를 오버라이딩 하는 경우, 컴파일러는 해당 클래스를 위해 vtable(virtual table)을 만들게 된다.

이 vtable은 클래스 내의 가상 함수의 함수 포인터를 포함한다.

각 클래스에는 한 개의 vtable만 존재하며, 동일 클래스의 모든 객체는 동일한 vtable을 공유한다.

![Screen Shot 2022-05-31 at 10.39.14 PM.png](https://user-images.githubusercontent.com/46529663/171388325-0b4682d3-0299-4298-b265-07ee6a493472.png)

virtual 키워드를 사용하여 위와 같이 기반(Base) 클래스와 그를 상속받는 파생(Derived) 클래스를 선언하고, main문에서 사용하면 GDB에서는 위와 같이 vtable이 구성된다.

그 후, 위에서 설명한 것과 같이 런타임에 vtable을 참조하여 오버라이딩된 함수를 실행한다.

위 사진을 설명하면, Base 클래스의 vtable에는 3개의 함수 포인터가 있다.
모두 기반 클래스에서 virtual 키워드를 추가한 함수로, 2개는 소멸자, 1개는 method 함수의 포인터이다.

가상 소멸자는 한 쌍을 이루는데, 위에서 첫 번째 소멸자를 `complete object destructor` 라고 하며, delete를 호출하지 않고 삭제될 때 호출되는 소멸자이다. 두 번째 소멸자는 `deleting destuctor` 라고 하며, delete를 사용하여 객체를 파괴할 때 호출된다.

추가적인 개념

- 추상 클래스(Abstract class)
- 순수 가상 함수(Pure virtual function)

[Virtual function - Wikipedia](https://en.wikipedia.org/wiki/Virtual_function)

[Demystifying Virtual Tables in C++ - Part 3 Virtual Tables | MartinKysel.com](https://www.martinkysel.com/demystifying-virtual-tables-in-c-part-3-virtual-tables/)

[[ELF] 1. ELF 란?](https://doitnow-man.tistory.com/225)