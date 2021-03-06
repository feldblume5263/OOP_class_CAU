# [C++] 객체지향 디자인

<br>

****

<br>

디자인 방법에 대해서 공부하기 전에, <br>

객체지향 프로그래밍 기술 중 하나인, **책임 주도 설계**에 대해서 알아보자.<br>

여기서 책임 주도 설계란 다음과 같이 이해할 수 있다.

```
"지금까지 살펴본 내용의 요점은 협력을 설계하기 위해서는 책임에 초점을 맞춰야 한다는 것이다. 어떤 책임을 선택하느냐가 전체적인 설계의 방향과 흐름을 결정한다. 이처럼 책임을 찾고 책임을 수행할 적절한 객체를 찾아 책임을 할당하는 방식으로 협력을 설계하는 방법을 책임 주도 설계(Responsibility-Driven Design, RDD)라고 부른다."
[오브젝트 / 조영호 저 / 위키북스 / 2쇄 2019년 07월 17일]

책임 주도 설계 방법의 과정은 다음과 같다.

시스템이 사용자에게 제공해야 하는 기능인 시스템 책임을 파악한다.
시스템 책임을 더 작은 책임으로 분할한다.
분할된 책임을 수행할 수 있는 적절한 객체 또는 역할을 찾아 책임을 할당한다.
객체가 책임을 수행하는 도중 다른 객체의 도움이 필요한 경우 이를 책임질 적절한 객체 또는 역할을 찾는다.
해당 객체 또는 역할에게 책임을 할당함으로써 두 객체가 협력하게 한다.
```

출처: [책임주도설계](https://johngrib.github.io/wiki/responsibility-driven-design/ )

<br>

객체지향 프로그램은 각각의 오브젝트들의 상호작용의 일련이다.<br>

각각의 오브젝트들은 책임을 가지고 있다. 시스템은 실행되어야 하는 여러가지 기능으로 나눠져 있다. 그리고 그 기능들은 시스템의 오브젝트들에 분산되어 있다.<br>

책임들의 리스트를 작성한후, 우리는 어떤 오브젝트에 어떤 책임을 부여해야 하는지를 결정해야 한다.<br>

다음은 디자인 중 한가지 예시이다. 디자인은 이런 것들을 고려하는 것이라는 정도만 알아두면 좋을 것 같다. <br>

<br>

<br>

## 0. 디자인 방법 개요

<br>

우리의 시스템이 무엇인지에 대한 어떤 설명을 가지고 있다고 생각해보자. <br>

그 기술서는 부정확하고, 모호하다. 이것은 단지 기술일 뿐이다.<br>

우리는 디자인 방법을 통해 **구체적인 논리**를 확립해야 한다.<br>

<br>

#### 개발 방법

##### 분석 단계

1. (Initial Description) 초기에 우리가 다루고자 하는 요인이 무엇인지를 설명한다.
2. (Refine Specification) 문제를 더욱 세세하게 다듬는다.

##### 디자인 단계

1. (Identification of Componetes) 필요한 요소들을 파악한다.
2. (Identification of Components Responsibilites) 각각 요소들이 가져야 할 책임을 파악한다.
3. (Formalize the Interface) 인터페이스를 구성한다.
4. (Designing the subsystem) 서브 시스템을 설계한다.

##### 구현 단계

1. (Implementation components) 요소들을 구현한다.
2. (Integration of components) 요소들을 통합한다.

##### 유지 단계

1. (Maintenance & Evolution) 유지, 개발

<br>

우리가 IIKH(Intelligent Interatctive Kitchen Helper) 프로그램을 만든다고 가정해보자.<br>

<br>

<br>

## 1. Initial Description

<br>

- 간단하게, IIKH는 PC기반의 프로그램이다.
  ![Description](https://github.com/feldblume5263/OOP_class_CAU/blob/master/other_materials/iikh_description.png?raw=true)
- 설명이 있지만, 여전히 모호하고 불분명하다.
- 우리는 설명에서 모호한 점들을 명확히 할 필요가 있다.

<br>

<br>

## 2. Refine Specification

<br>

- 실제로 제품을 사용하고 가정하고, 좀 더 프로그램을 세세하게 이해해야 한다.
  ![Refine Specification](https://github.com/feldblume5263/OOP_class_CAU/blob/master/other_materials/refine%20specification.png?raw=true)

- 다음 작업들을 통해 IIKH의 세세한 기능들을 파악한다.

  1. 레시피 데이터베이스 탐색 (두가지 이상의 재료들로도 가능해야 함.)

  2. 새로운 레시피를 데이터베이스에 추가하기

  3. 기존 레시피에 주석 달기

  4. 여러가지 요리로 된 식사를 계획하기

  5. 일주일과 같은 더 긴 기간의 식사도 계획하기

  6. 전체 기간의 메뉴에 대한 식료품 리스트 작성하기

  등등...

<br>

<br>

## 3. Identification of Componetes

<br>

- 구성요소에 대해 파악해야 한다.

- CRC 카드
  CRC카드를 통해 쉽게 구성요소를 파악할 수 있다.<br>
  ![CRC](https://github.com/feldblume5263/OOP_class_CAU/blob/master/other_materials/crc.png?raw=true)

- 구성요소

  IIKH는 다음의 6개 구성요소로 파악해볼 수 있다.<br>

  [Greeter] [Recipe Database] [Recipe] [Meal] [Plan Manager] [Date]<br>

<br>

<br>

## 4. Identification of Components Responsibilites

<br>

#### 메인화면 구성요소

- 응용프로그램이 시작하면, 친숙한 인삿말로 시작하기

- 그리고 나서 다음의 동작들이 가능해야 한다.

- 레시피 데이터베이스를 가볍게 검색가능해야 함. (두가지 이상의 식재료로도)

- 새 레시피 추가

- 레시피 편집 또는 주석 달기

- 여러 식사 계획 검토

- 식사 계획 세우기

<br>

#### 데이터베이스 구성요소

- 레시피 데이터베이스를 유지해야 함

- 사용자가 데이터베이스를 탐색 할 수 있도록 허용해야 함.

- 사용자가 기존 레시피를 편집하거나 주석을 달 수 있도록 허용해야 함.

- 사용자가 새 레시피를 추가 할 수 있도록 허용해야 함.

<br>

#### 레시피에 대한 역할들

- 성분 목록 및 변형 알고리즘 유지 (프로그램 종료 후에도 변경된 자료가 남아있어야 한다.)

- 데이터 값들을 편집하는 방법을 알아야한다.

- 출력 장치에 상호작용적으로 표시하는 방법을 알아야 한다.

- 출력 기기로 인쇄하는 방법을 알아야 한다.

<br>

#### 플래너 구성요소

- 사용자가 계획을 위해 특정 날짜를 선택할 수 있어야 한다.

- 사용자가 기존 계획을 편집 할 수 있도록 해야 한다.

- Date 객체와의 연결

<br>

#### 날짜 구성요소

- 사용자가 특정 식사를 편집 할 수 있어야 한다.

- 사용자는 날짜에 대한 정보에 주석을 달 수 있어야 한다. (생일이나, 크리스마스 저녁 같은)

- 전체 식사들에 대한 식료품 목록을 인쇄 할 수 있어야 한다.

<br>

#### 식사 구성요소

- 단일 식사에 대한 정보를 보유해야 함.
  - 사용자가 조리법 데이터베이스와 상호 작용하여 식사에 대한 개별 조리법을 선택할 수 있어야 한다.
  - 사용자가 식사에 참석할 인원 수를 설정하면 레시피가 자동으로 조정되야 한다.

  - 개별 레시피들의 식료품 목록을 결합하여 전체 식사에 대한 식료품 목록을 생성 할 수 있어야 함.

<br>

<br>

## 5. Formalize the Interface

<br>

| Interface Veiw | Implementation View              |
| -------------- | -------------------------------- |
| public View    | Private View (purposeful hiding) |

<br>

<br>

## 6. Designing the subsystem

<br>

