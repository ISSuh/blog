---
title: Effective C++ - Item.7
date: 2020-05-04 13:18:00
categories:
- C++
tags:
- C++
- Effective C++
---

# 다형성을 가진 기본 클래스에서는 소멸자를 반드시 가상 소멸자로 선언하자

---

## 내용

### 가상 소멸자

C++의 규정에 의하면, 기본 클래스 포인터를 통해 파생 클래스 객체가 삭제 될때, 그 기본 클래스에 비가상 소멸자가 있으면 프로그램 동작은 미정의 사항이라고 되어 있다. 대개 그 객체의 파생 클래스 부분이 소멸되지 않게 된다.

이러한 문제를 해결하기 위한 해결방법으로는 간단하게 기본클래스의 소멸자를 가상 소멸자로 선언하는 것이다.

```cpp
class Base {
public:
  virtual ~Base();    // 가상 소멸자 선언

  ...

};

class Derived : public Base { ... }
```

일반적으로, 가상 함수를 하나라도 가진 클래스는 가상 소멸자를 가져야 하는 것이 대부분 맞는 말이다.

어느 경우를 막론하고, 소멸자를 전부 virtual로 선언하는 일은 virtual로 절대 선언하지 않는 것만큼이나 좋지 않은 생각이다. 가상 소멸자를 선언하는 것은 그 클래스에 가상 함수가 하나라도 들어있는 경우에만 한정하는 것이 좋다.

### Virtual Table

가상 소멸자를 가지고 있지 않은 클래스를 만나면 컴파일러는 '저 클래스는 기본 클래스로 쓰이지 않는 클래스 구나' 라고 생각한다. 반대로 생각해도 마찬가지 인데, 기본 클래스로 의도하지 않은 클래스에 대해 가상 소멸자를 선언하는 것은 좋지 않은 경우이다.

```cpp
class Point {
public:
  Point(int xCoord, int yCoord);
  ~Point();

private:
  int x, y;
};
```

int가 32비트를 차지한다고 가정하면, 이 Point 객체는 64비트 레지스터에 딱 맞게 들어 갈수 있을 것이다. 그런데, Point 클래스가 가상 소멸자로 들어가게 되는 순간, 사정이 변하게 된다.

가상 함수를 C++에서 구현하려면 클래스에 별도의 자료구조가 하나 더 들어가야 한다. 이 자료구조는 프로그램 실행 중에 주어진 객체에 대해 어떤 가상 함수를 호출해야 하는지를 결정하는데 쓰이는 정보인데, 실체로는 포인터의 형태를 가지는 것이 대부분이고, 대개 **vptr(Virtual Table Pointer)** 이라는 이름으로 불린다. *vptr*은 가상함수의 주소, 즉 포인터들의 배열을 가리키고 있으며 가상 함수 테이블 포인터의 배열은 **vtbl(Virtual Table)** 이라고 불린다.

가상함수를 하나라도 가지고 있는 클래스는 반드시 그와 관련된 *vtbl*을 가지고 있다. 어떤 객체에 대해 어떤 가상함수가 호출되려고 하면, 호출되는 실제 함수는 그 객체의 *vptr*이 가르키는 *vtbl*에 따라 결정된다. *vtbl*에 있는 함수 포인터들 중 적절한 것이 연결되는 것이다.

가장 중요한 것은 예제 Point 클래스에 가상 함수가 들어가게 되면, Point 타입 객체의 크기가 커진다는 점이다. 프로그램 실행환경이 32비트 아키텍처라면, 크기가 64비트(int 두개)에서 96비트(int 두개에 *vpt*r하나)로 커지게 된다. 64비트 아키텍처에서는 포인터 크기는 64비트이므로, Point 객체의 크기가 64비트에서 128비트로 커질 수 있다.

Point 객체는 가상 함수 테이블 포인터가 하나 추가되었을 뿐인데 크기가 무려 50% 에서 100% 까지 커지게 된다. 또한 C 등의 다른 언어로 선언된 동일한 자료구조와도 호환성이 없어지게 된다. 왜냐하면 다른 언어로 Point와 겉보기가 똑같은 데이터 배치를 써서 선언했다고 해도 *vptr*만은 어떻게 만들 수 없기 때문이다. 결국, 다른 언어로 작성된 함수에 Point 객체를 전달하고 또 그 함수로부터 전달받을 수 있게 하려면 *vptr*부분을 어떻게든 보충해 주어야 하는데, 이 부분부터는 구현환결에 따라 세부사항이 달라지는 문제이기 때문에 이식성에 대한 기대는 할 수 없게 된다.

### 가상 소멸자가 없는 클래스들

가상함수가 전혀 없는데도 비가상 소멸자 때문에 함정에 빠지는 경우도 있다. 한 예가 표준 string 타입이다. 이 타입은 가상함수를 가지고 있지 않지만, 전후 사정을 무시하고 이 타입을 기본 클래스로 잡아버리는 일부 프로그래머가 있다.

```cpp
// std::string 에는 가상 소멸자가 없다
class MyString : public std::string { ... }

...

MyString* pss = new MyString("Hello World");
std::string *ps;

ps = pss;         // MyString* ==> std::string*

delete ps;        // 정의되지 않은 동작이 발생한다
                  // 실질적으로는 *ps의 MyString 부분에 있는 자원이 누출되는데,
                  // 그 이유는 MyString의 소멸자가 호출되지 않기 때문이다
```

위와 같은 현상은 가상 소멸자가 없는 클래스면 어떤 것에는 전부 적용 된다. string과 같은 STL 컨테이너 타입 전부가 여기에 속한다.

#### 순수 가상 소멸자

경우에 따라 순수 가상 소멸자를 두면 편리하게 사용 할 수도 있다. 순수 가상 함수는 해당 클래스를 **추상 클래스(Abstract Calss : 그 타입의 객체를 생성할 수 없는)** 로 만든다. 하지만 어떤 클래스가 추상 클래스였으면 좋겠는데 마땅히 넣은 만할 순수 가상 함수가 없을 때도 종종 생기게 된다.

추상 클래스는 본래 기본 클래스로 쓰일 목적으로 만들어진 것이고, 기본 클래스로 쓰이려는 클래스는 가상 소멸자를 가져야 한다. 한편 순수 가상 함수가 있으면 바로 추상 클래스가 된다. 종합해보면, 추상 클래스로 만들고 싶은 클래스에 순수 가상 소멸자를 선언하는 것이다.

```cpp
class AWOV {
public:
  virtual ~AWOV() = 0;

  ...

};
```

AWOV 클래스는 순수 가상 함수를 가지고 있으므로, 우선 추상 클래스이고, 순수 가상 함수가 가상 소멸자 이므로 앞에서 말한 소멸자 호출 문제로 고민할 필요가 없어지게 된다. 그러나 한가지 짚고 넘어가야 하는 것은, 이 순수 가상 소멸자의 정의를 두지 않으면 안된다는 것이다.

```cpp
// 순수 가상 소멸자의 정의
AWOV::~AWOV() {}
```

소멸자가 동작하는 순서는, 상속 계통 구조에서 가장 말단에 있는 파생클래스의 소멸자가 먼저 호출되는 것을 시작으로, 기본 클래스 쪽으로 거쳐 올라가면서 각 기본 클래스의 소멸자가 하나씩 호출된다. 컴파일러는 ~AWOV의 호출 코드를 만들기 위해 파생 클래스의 소멸자를 사용할 것이므로, 잊지 말고 이 함수의 본문을 준비해 두어야 하는 것이다. 만약 이부분을 잊으면 링커 에러가 발생하게 된다.

### 소멸자와 다형성

기본 클래스 안에 가상 소멸자를 선언하자는 규칙은 *다형성(Polymorphic)* 을 가진 기본 클래스, 즉 기본 클래스 인터페이스를 통해 파생 클래스 타입의 조작을 허용하도록 설계된 기본 클래스에만 적용 된다.

모든 기본 클래스가 다형성을 가지게 되도록 설계되는 것은 아니다. 앞에서 언급된 string 타입과 , STL 컨테이너 타입과 같이 기본 클래스는 커녕 다형성의 흔적조차 볼 수 없는 클래스도 존재한다. 한편, 기본 클래스로는 쓰일수 있지만 다형성은 가지지 않도록 설계된 클래스도 존재하는데, 이런 클래스는 기본 클래스의 인터페이스를 통한 파생 클래스 객체의 조작이 허용되지 않는다. 이들에게서 가상 소멸자를 볼 수 없는 것은 이러한 이유 때문이다.

## 요점

> 다형성을 가진 기본 클래스에는 반드시 가상 소멸자를 선언해야 한다. 즉, 어떤 클래스가 가상 함수를 하나라도 가지고 있다면, 이 클래스의 소멸자도 가상 소멸자 이여야 한다.

> 기본 클래스로 설계되지 않았거나 다형성을 가지도록 설계되지 않은 클래스에는 가상 소멸자를 선언하지 말아야 한다.

---
---
*참고*. Effective C++ 3/E - Scott Meyers

---