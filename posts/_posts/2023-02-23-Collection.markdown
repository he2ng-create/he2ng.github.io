---
layout: single
title:  "Collection Framework"
date:   2023-02-03 00:00:00
categories: java
---
# 0. Overview
Java에서 제공하는 Collections Framework를 이해하고 사용할 수 있는 걸 목적으로 합니다.

이번 주요 목표는 다음과 같습니다.

* Collections Framework을 이해하고 종류를 압니다.
* Collections 차이를 이해합니다.
* Collections API를 사용 예를 알아봅니다.

# 1. Collections Framework과 Collection Framework의 종류
컬렉션 프레임웍이란, 데이터 군을 저장하는 클래스들을 표준화한 설계 입니다. 데이터 그룹을 다루기 위해 등장하였고 프레임웍은 표준화된 프로그램 방식을 의미합니다. 즉, 데이터 그룹을 다루기 위한 표준이 필요했고 Java API에서 해당 표준들을 제공합니다.

## 종류

|인터페이스|특징|
|-------|---|
|List|순서가 있는 데이터의 집합. 중복 허용.|
|Set|순서를 유지하지 않는 데이터 집합. 중복 허용 안함.|
|Map|key와 value로 이루어진 데이터 집합 <br> key는 중복 허용 안함. value는 중복 허용함.|

컬렉션 인터페이스간의 상속 계층도:<br>
![컬렉션 인터페이스간의 상속 계층도](https://iamhe2ng.github.io/he2ng.github.io/assets/images/posts/collection.png)

> NOTE : List와 Set을 구현한 구현체들은 공통점이 많아서 Collection 인터페이스로 뽑아 정의할 수 있음.
>
> Map의 경우 key, value 형태이기때문에 별도로 인터페이스 존재.

# 2. Collections Framework 구현체의 차이점 

## Arrays와 List 차이

| 종류         | Arrays                      | List                                |
|------------|-----------------------------|-------------------------------------|
| 사이즈        | 초기화 시 고정                    | 동적 구성                               |
| 사이즈 변경 여부  | 사이즈 변경 불가                   | 추가, 삭제 가능                           |
| 속도         | 초기화 시 메모리 할당되어 List보다 속도 빠름 | 배열 추가 삭제 시 메모리에 재할당. Arrays보다 속도 느림 |
| 요소         | primitive type, Object      | Object                              |
| 요소 할당      | assignment(할당)              | add(추가)                             |
| 지네릭스 사용 여부 | 불가능                         | 가능                                  |


### Arrays 선언과 초기화 
```java
// 선언
type[] arrayName;
type arrayName[];

// 생성 
arrayName = new type[length];

// 선언과 생성
type[] arrayName = new type[length];

// 초기화
int[] odds = {1, 3, 5, 7, 9};
String[] alphabet = {"A", "B", "C"};
Person[] people = { new Person("he2ng", 20) };
```

### ArrayList 선언과 초기화
ArrayList는 List 인터페이스를 상속받은 클래스로 크기가 가변적으로 변하는 선형 리스트입니다.

```java
// List의 인터페이스 사용 ( SOLID -> 리스코프 치환 원칙 )
final List<Person> people = new ArrayList<Person>();

// 컴파일 시점에 타입 추론 가능하여 new ArrayList<Person> -> Person 생략 가능 
final ArrayList<Person> people1 = new ArrayList<>();
```

## ArrayList와 LinkedList 차이와 사용처 

| 종류 | 특징                          |
|-----|------------------------------|
| ArrayList | 1. 크기를 변경할 수 있다. <br> 2. 읽기(접근 시간) 빠르다 <br> 3. 데이터 추가/삭제가 느리다.|
| LinkedList | 1. 크기를 변경할 수 없다. <br> 2. 읽기(접근 시간) 느리다 <br> 3. 비순차적인 데이터의 추가 또는 삭제에 시간이 많이 걸린다. |

다루는 데이터의 개수가 변하지 않은 경우라면 `ArrayList`

데이터 개수의 변경이 잦다면 `LinkedList`

## HashMap과 HashSet 차이

| 종류 | 특징  |
|----|-------|
|HashMap|Key는 중복 허용 안함, Value(요소) 중복 허용함|
|HashSet|Key는 중복 허용 안함, Value(요소) 중복 허용 안함| 

> NOTE : Hash란? 해시 함수 또는 해시 알고리즘을 통해 얻어지는 고정된 길이의 해시 값(해시 코드) 
>
> 해시 테이블이라는 자료구조에서 사용되며, 매우 빠른 데이터 검색을 위해 사용됨.


# 3. Collection API 사용 예
자주 사용하는 Collection API 를 정리한다.

| Modifier and Type | Method and Description  |
|---|----|
|boolean|`add(E e)`<br>단일 요소 추가 (Optional) * 중복 요소 허용안하는 경우 (e.g. Set..)|
|boolean|`addAll(Collection<? Extends E> c)`<br> 컬렉션의 모든 요소를 이 컬렉션에 추가 (Optional)|
|boolean|`clear()`<br> 컬렉션에서 모든 요소 제거|
|boolean|`contains(Object o)`<br> 컬렉션에 지정된 요소가 있는 지 확인하여 true, false 반환|
|boolean|`isEmpty()`<br> 컬렉션이 비었는 지 확인하여 true, false 반환
|Iterator<E>|`iterator()`<br>컬렉션의 요소에 대한 반복자 반환. (가끔 사용)|
|default Stream<E>|`parallelStream()`<br> 병렬 처리 가능한 Stream 반환|
|boolean|`remove(Object o)`<br> 지정된 요소가 있는 경우 컬렉션 내의 지정된 요소의 단일 인스턴스 제거
|boolean|`removeAll(Collection<?> c)`<br> 지정된 컬랙션이 컬랙션 내에 포함 된 경우 해당 요소들 제거|
|boolean|`removeIf(Predicate<? super E> filter)`<br> 컬랙션 내에서 지정된 조건자를 충족하는 경우 요소들은 제거|
|int|`size()`<br> 컬렉션의 요소 수(사이즈) 반환|
|default Stream<E>|`stream()`<br> 컬렉션을 순서로 하는 Stream 반환|
