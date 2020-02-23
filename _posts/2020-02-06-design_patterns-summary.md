---
title: Design Patterns - Summary
date: 2020-02-06 23:45:00
categories:
- Design Patterns
tags:
- Design Patterns
- C++
---

# Design Patterns - Summary

## 디자인패턴이란?
> “바퀴를 다시 발명하지 마라(Don’t reinvent the wheel)”

> **많은 다른 상황이나 어플리케이션에서 발생하는 문제를 해결하는 방법에 대한 템플릿**

객체 지향 프로그래밍 설계를 할 때 자주 발생하는 문제들을 피하기 위해 사용되는 패턴.
이미 수많은 개발자들이 현재 고민중인 문제와 유사한 문제를 해결하기위해 고민하였고, 이러한 문제 혹은 상황에 자주 쓰이는 해결방법을 패턴화 하여 해결책을 제시한다. 
다만 주의 할점은 디자인패턴이 만능은 아니다. 디자인패턴은 알고리즘이 아닌 단순히 문제를 해결하기위한 설계상의 패턴이기 때문에, 단순한 방법론일 뿐이다.
따라서 디자인패턴이 어떠한 상황에 필요한지, 왜 효율적인지 이해하고 사용하는 것이 중요하다.

  - 장점
    - 개발자 간의 원활한 의사소통
    - 소프트웨어 구조 파악 용이
    - 재사용을 통한 개발 시간 단축
    - 설계 변경 요청에 대한 유연한 대처

  - 단점
    - 객체지향 설계/구현 위주로 사용된다.
    - 초기 투자 비용 부담.

## 디자인 패턴 구조

  - 콘텍스트(context)
      - 문제가 발생하는 여어 상황을 기술한다. 즉, 패턴이 적용될 수 있는 상황을 나타낸다. 
      경우에 따라서는 패턴이 유용하지 못한 상황을 나타내기도 한다.
  - 문제(problem)
      - 패턴이 적용되어 해결될 필요가 있는 여러 디자인 이슈들을 기술한다.
        이때 여러 제약 사항과 영향력도 문제 해결을 위해 고려해야 한다.
  - 해결(solution)
      - 문제를 해결하도록 설계를 구성하는 요소들과 그 요소들 사이의 관계, 책임, 협력 관계를 기술한다.
        해결은 반드시 구체적인 구현 방법이나 언어에 의존적이지 않으며 다양한 상황에 적용할 수 있는 일종의 템플릿이다.

## 디자인패턴의 종류

23가지의 디자인 패턴을 정리하고 각각의 디자인 패턴을 생성(Creational), 구조(Structural), 행위(Behavioral) 3가지로 분류했다

  - Creational Patterns (생성패턴)
    - Builder 
    - Factory
    - Abstract Factory
    - Prototype
    - Singleton
    
  - Structural Patterns (구조패턴)
    - Adapter
    - Bridge
    - Composite
    - Decorator
    - Facade
    - Flyweight
    - Proxy
    - Curiously Recurring Template
    - Interface-based Programming (IBP)

  - Behavioral Patterns (행동패턴)
    - Chain of Responsibility
    - Command
    - Interpreter
    - Iterator
    - Mediator
    - Memento
    - Observer
    - State
    - Strategy
    - Template Method
    - Visitor
    - Model-View-Controller (MVC)

![design_patterns](https://gmlwjd9405.github.io/images/design-pattern/types-of-designpattern.png)

## Creational Patterns (생성패턴)
 > **객체의 생성을 위한 패턴**
 
상황에 적합한 방식으로 객체를 생성하려고 한다. 객체 생성의 기본 형태는 설계 문제를 야기하거나 설계에 복잡성을 가중시킬 수 있다. 
창조적인 디자인 패턴은 이 객체 창조를 어떻게든 제어함으로써 이 문제를 해결한다.

## Structural Patterns (구조패턴)
 > **클레스와 객체을 조합하여 더큰 구조를 만드는 패턴**
 
서로 다른 인터페이스를 지닌 2개의 객체를 묶어 단일 인터페이스를 제공하거나 객체들을 서로 묶어 새로운 기능을 제공하는 패턴이다.

## Behavioral Patterns (행동패턴)
 > **클래스와 객체사이의 행동 및 책임에 관한 패턴**

한 객체가 혼자 수행할 수 없는 작업을 여러 개의 객체로 어떻게 분배하는지, 또 그렇게 하면서도 객체 사이의 결합도를 최소화하는 것에 중점을 둔다.

