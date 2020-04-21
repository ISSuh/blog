---
title: Design Patterns - Command
date: 2020-04-21 21:27:00
categories:
- Design Patterns
tags:
- Design Patterns
- Behavioral Patterns 
- Command
- C++
---

# Behavioral Patterns - Command

## Intent

---

요청 자체를 캡슐화하는 것이다. 이를 통해 요청이 서로 다른 사용자를 매개변수로 만들고, 요청을 대기시키거나 로깅하여, 되돌릴 수 있는 연산을 지원한다.

작동(Action), 트랜젝션(Transaction) 이라고도 불린다.

## Utility

---

#### 수행할 동작을 객체로 매개변후과 하고자 할 때

콜백함수를 구현하여 매개변수화를 표현할 수 있다.

#### 서로다른 시간에 요청을 명시하고, 저장하며, 실행하고 싶을 때

요청을 받아 처리하는 객체가 주소 지정 방식과는 독립적으로 표현될 수 있다면, *Command* 객체를 다른 프로세스에게 넘겨주고 거기서 해당 처리를 진행 할 수 있다.

#### 실행 취소 기능을 지원하고 싶을 때

*Command*의 *Excute()* 연산은 상태를 저장할 수 있는데, 이를 이용해서 지금까지 얻은 결과를 바꿀 수 있다.

실행된 명령어를 모두 기록해 두었다가 이 리스트를 역으로 탐색하여 다시 *Command* 클래스 내에 정의된 *UnExcute()* 연산을 통해 수행 취소를 한다.  

#### 시스템이 고장 났을 떄 재적용이 가능하도록 변경 과정에 대한 로깅을 지원하고 싶을 떄

*Command* 인터페이스를 확장하여 *Load()* 와 *Store()* 연산을 정의하면 상태의 변화를 지속적(persistent) 저장소에 저장해 둘 수 있다.

시스템 장애가 발생했을떄, 해당 저장소에서 저장된 명령어를 읽어 다시 *Excute()* 연산을 통해 재실행 하면 된다.

#### 기본적은 연산의 조합으로 만든 상위 수준의 연산을 써서 시스템을 구조화하고 싶을 떄

정보 시스템의 일반적인 특성은 **트랜잭션(Transaction)**을 처리해야 한다는 것이다. 트랜잭션은 일련의 과정을 통해 데이터를 변경하는 것이다. *Command Pattern*은 이런 트랜잭션의 모델링을 가능하게 한다.

*Command* 클래스는 일관된 인터페이스를 정의하는데, 이로써 모든 트랜잭션이 동일한 방식으로 호출된다.

새로운 트랜잭션을 만들면 상속으로 *Command* 클래스를 확장하면 되므로 시스템 확장도 어렵지 않게 가능하다.

## Structure

---

### Basic Structure

![example](http://www.cs.unc.edu/~stotts/GOF/hires/Pictures/command.gif)

### Structure Example

![example](http://www.cs.unc.edu/~stotts/GOF/hires/Pictures/comma081.gif)

![example](http://www.cs.unc.edu/~stotts/GOF/hires/Pictures/comma078.gif)

![example](http://www.cs.unc.edu/~stotts/GOF/hires/Pictures/comma080.gif)

![example](http://www.cs.unc.edu/~stotts/GOF/hires/Pictures/comma079.gif)

### Elements

- **Command**
  - 연산 수행에 필요한 인터페이스를 선언
- **ConcreteCommand**
  - *PasteCommand*, *OpenCommand* 에 해당
  - *Receiver* 객체와 액션 간의 연결성을 정의
  - 처리 객체에 정의된 연산을 호출하도록 *Excute()* 연산을 구현
- **Client**
  - *Appilication* 에 해당
  - *ConcreteCommand* 객체를 생성하고 처리 객체로 정의
- **Invoker**
  - *MenuItem* 에 해당
  - *Command Pattern* 에 처리를 수행할 것을 요청
- **Receiver**
  - *Document*, *Appilication* 에 해당
  - 요청에 관련된 연산 수행 방법을 저장
  - 어떤 클래스도 요청 수신자로써 동작 가능

사용자는 *ConcreteCommand* 객체를 생성하고 이를 수신자로 지정한다.

*Invoker* 클래스는 *ConcreteCommand* 객체를 저장한다.

*Invoker* 클래스는 *Command*에 정의된 *Excute()*를 호출하여 요청을 발생시킨다. 명령어가 취소기능이 가능하다면, *ConcreteCommand*는 이전에 *Excute()* 호출 전 상태의 취소 처리를 위해 저장한다.

*ConcreteCommand* 객체는 요청을 실체 처리할 객체에 정의된 연산을 호출한다.

다음 다이어그램은 협력자 사이의 상호작용을 보여준다.

![example](http://www.cs.unc.edu/~stotts/GOF/hires/Pictures/comma077.gif)

*Command* 객체로 요청 발생자(*Invoker*)가 요청 수신자에서 분리된다.  

## Feature

---

- *Command*는 연산을 호출하는 객체와 연산 수행 방법을 구현하는 객체를 분리한다.
- *Command*는 일급 클래스이다. 다른 객체와 같은 방식으로 조작되고 확장할 수 있다.
- 명령을 여러 개로 복합해서 복합 명령을 만들 수 있다.
  - *Composite Pattern*으로 요로 명령어를 구성할 수 있다.
- 새로운 *Command* 객체를 추가하기 쉽다.
  - 기존 클래스를 변경할 필요 없이 단지 새로운 명령어에 대응하는 클래스만 정의하면 된다.

## Implementation

---

### Implement Example

```cpp

/**
* @brief Handler - 
* @details
*/

...



...

```

## Related Pattern

---


---
---
*참고*. Design Patterns : Elements of Reusable Object-Oriented Software - Erich Gamma

---
