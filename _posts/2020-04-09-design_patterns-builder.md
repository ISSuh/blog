---
title: Design Patterns - Builder
date: 2020-04-09 20:52:00
categories:
- Design Patterns
tags:
- Design Patterns
- C++
- Builder
---

# Creational Patterns - Builder

## Intent

복잡한 객체를 생성하는 방법과 표현하는 방법을 정의하는 클래스를 별도로 분리하여, 서로 다른 표현이라도 이를 생성할 수 있는 동일한 절차를 제공할수 있도록 함

## Utility

- 복합 객체를 생성하는 알고리즘이 객체를 구성하는 요소 부분과 이들을 조립하는 방법에 독립적일 때
- 구성할 객체들의 표현이 서로 다르더라도 생성 절차에서 이를 지원해야 할 때

## Structure
![example](https://online.visual-paradigm.com/repository/images/2c05a648-7626-4cca-abae-6c948dd43b14.png)

### Elements
  
- **Builder**
  - *Product* 객체의 일부 요소들을 생성하기 위한 추상 인터페이스를 정의
- **ConcreteBuilder**
  - *Builder* 클래스에 정의된 인터페이스를 구현하고, *Product* 의 부품들을 모아 *Builder* 를 구성
  - 생성한 요소의 표현을 정의하고 관리
  - 제품을 검색하기 위한 인터페이스를 제공
- **Director**
  - *Builder* 인터페이스를 사용하는 객체를 구성
- **Product**
  - 생성할 복합 객체를 표현
  - *ConcreteBuilder* 는 *Product* 의 내부 표현을 구축하고, 복합 객체가 어떻게 구성되는지에 대한 절차를 정의

### Diagram

![example](http://www.cs.unc.edu/~stotts/GOF/hires/Pictures/build095.gif)

## Feature

- 제품에 대한 내부 표현을 다양하게 변화 가능
  - *Builder* 를 사용하면 *Product* 이 어떤 요소에서 구성되는지, 그리고 각 요소들의 표현방법이 무엇인지 판단 가능하다.
  - 새로운 *Product* 의 표현 방법이나 구성 방법이 변경되면, 이에 대하여 *Builder* 클래스의 서브 클래스를 정의하면 된다.
- 생성과 표현에 대한 코드를 분리
  - 복합 객체의 생성과 내부 표현 방법을 별도의 모듈로 관리 가능하다,
  - *ConcreteBuilder* 는 특정 종류의 *Product* 을 생성하고 조립하는데 필요한 모든 연산을 포함한다. 
- 복합 객체를 생성하는 절차의 세분화
  - 복합 객체를 생성할 떄, *Director* 의 통제 아래 하나씩 내부 구성요소를 만들어 나간다.
  - *Builder* 클래스의 인터페이스에는 *Product* 를 생성하는 과정 자체가 반영되어 있다.

## Implementation
 
```cpp
////////////////////////////////////////////////////////////////////////////////
// Product
////////////////////////////////////////////////////////////////////////////////
class Person {
public:
  void setName(const std::string& name) { m_name = name; }
  void setAge(const int age)            { m_age = age; }
  void setTeam(const std::string& job)  { m_job = job; }

  void printInfo() const {
    std::cout << m_name << " / "<< m_age << " / "<< m_team << " / " << std::endl;
  }

private:
  std::string m_name; 
  int m_age;
  std::string m_team; 
};

////////////////////////////////////////////////////////////////////////////////
// Builder(AbstractBuilder)
////////////////////////////////////////////////////////////////////////////////
class PersonBuilder {
public:
  virtual ~PersonBuilder() {}

  void createNewPerson() const { 
    return new Person(); 
  }

  Person* getPerson() const { 
    return m_person; 
  }

  virtual void buildName(const std::string& name) = 0;
  virtual void buildAge(const int age) = 0;
  virtual void buildTeam() = 0;

protected:
  Person m_person;
};

////////////////////////////////////////////////////////////////////////////////
// ConcreteBuilder
////////////////////////////////////////////////////////////////////////////////
class DevelopmentPersonBuilder : public PersonBuilder {
public:
  void buildName(const std::string& name) override {
     m_person->setName(name);
  }

  void buildAge(const int age) override { 
    m_person->setAge(age); 
  }

  void buildTeam() override { 
    m_person->setTeam("Development"); 
  }
};

class SalesPersonBuilder : public PersonBuilder {
public:
  void buildName(const std::string& name) override { 
    m_person->setName(name); 
  }

  void buildAge(const int age) override { 
    m_person->setAge(age); 
  }

  void buildTeam() override { 
    m_person->setTeam("Sales"); 
  }
};

////////////////////////////////////////////////////////////////////////////////
// Director
////////////////////////////////////////////////////////////////////////////////
class Director {
public:
  void setBuilder(PersonBuild* personBuilder) {
    m_personBuilder = personBuilder; 
  }
  
  void construct(const std::string& name, const int age) const {
    m_personBuilder->createPerson();

    m_personBuilder->buildName(name);
    m_personBuilder->buildAge(age);
    m_personBuilder->buildJob();
  }

  Person* GetPerson() { 
    return m_personBuilder->getPerson(); 
  }

private:
  PersonBuild* m_personBuilder = nullptr;
};


...

  // product, builer, director 객체 생성
  Person* person = nullptr;
  Director director;

  // 상황에 따라 ConcreteBuilder 선택
  if(hireDeveloper())
    director.setBuilder(new DevelopmentPersonBuilder());
  else
    director.setBuilder(new SalesPersonBuilder());

  // 선택된 ConcreteBuilder 적용 및 객체 생성을 위한 매개변수 설정
  director.construct("Eddie", 29);
  
  // ConcreteBuilder에 맞춰 생성된 객체 적용
  person = director.GetPerson();

  person.printInfo();

...

```

---
---
*참고*. Design Patterns : Elements of Reusable Object-Oriented Software - Erich Gamma

---
