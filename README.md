# SE443 Tutorial: Mocking with Mockito

## Overview

Production classes rarely work alone. They call databases, web services, repositories, and other objects. A unit test should focus on one class at a time, so it replaces those dependencies with **mocks**—controllable stand-ins that return predetermined values and record how they were used.

In this tutorial, you will use [Mockito](https://site.mockito.org/) with JUnit 4 to:

- create mock objects;
- stub method results;
- define consecutive return values;
- use argument matchers;
- test a class independently from its dependency; and
- explain the interaction between a class under test and a mock.

## Prerequisites

- Java 17 or later
- Maven 3.8 or later
- An IDE of your choice (optional)

Check your installation:

```bash
java -version
mvn -version
```

## Project structure

```text
.
├── pom.xml
├── src
│   ├── main/java/com/se465/mock
│   │   ├── TodoBusinessImpl.java
│   │   └── TodoService.java
│   └── test/java/com/se465/mock
│       ├── ListTestTest.java
│       └── TodoBusinessImplMockitoTest.java
└── README.md
```

`TodoBusinessImpl` is the class under test. `TodoService` is its dependency. The tests replace `TodoService` with a Mockito mock, so no real service implementation is required.

## Getting started

From the project root, run:

```bash
mvn clean test
```

Maven downloads JUnit and Mockito automatically. A successful run ends with `BUILD SUCCESS`.

To run one test class:

```bash
mvn -Dtest=ListTestTest test
mvn -Dtest=TodoBusinessImplMockitoTest test
```

## Part A — Understand the test setup

Open `pom.xml` and identify:

1. the Java version used to compile the project;
2. the JUnit dependency;
3. the Mockito dependency; and
4. why both testing dependencies use the `test` scope.

Unlike the original setup instructions, you do not need to create an Eclipse project or paste dependencies manually. The repository is already a standard Maven project.

## Part B — Mock a `List`

Open `src/test/java/com/se465/mock/ListTestTest.java` and run its four tests.

### 1. Stub one return value

`letsMockListSize` creates a mock `List` and defines the result of `size()`:

```java
when(list.size()).thenReturn(10);
```

The mock does not calculate a real list size. It returns the value specified by the test.

### 2. Stub consecutive return values

`letsMockListSizeWithMultipleReturnValues` demonstrates different results on consecutive calls:

```java
when(list.size()).thenReturn(10, 20);
```

The first call returns `10`; the second and later calls return `20`.

### 3. Observe Mockito's default answer

In `letsMockListGet`, only `get(0)` is stubbed. Uncomment the following assertion, rerun the test, and explain the result:

```java
assertNull(list.get(1));
```

For an unstubbed method, Mockito returns an appropriate default value—for example, `null` for many reference types, `0` for numeric primitives, and `false` for `boolean`.

### 4. Use an argument matcher

`letsMockListGetWithAny` uses `anyInt()` instead of a specific index:

```java
when(list.get(anyInt())).thenReturn("this is an int");
```

Run the test and explain why calls with both `0` and `1` match the same stub.

## Part C — Isolate a class from its dependency

Read these files in order:

1. `TodoService.java` — the dependency contract;
2. `TodoBusinessImpl.java` — the class under test; and
3. `TodoBusinessImplMockitoTest.java` — the isolated unit tests.

Trace the `usingMockito` test:

1. Mockito creates a `TodoService` mock.
2. The test stubs `retrieveTodos("Ranga")` with three sample items.
3. The mock is injected into `TodoBusinessImpl` through its constructor.
4. `retrieveTodosRelatedToSpring` asks the mock for the items.
5. The business class keeps only items containing `"Spring"`.
6. The test verifies the resulting list.

Then inspect `deletesOnlyTodosNotRelatedToSpring`. Notice the difference between:

- **state verification**, which checks a returned value with an assertion; and
- **interaction verification**, which checks whether the mock received the expected method calls with `verify(...)`.

## Questions you can answer!

Submit concise answers supported by relevant code snippets or test-output screenshots.

### Question 1

In `letsMockListGet`, does `assertNull(list.get(1))` pass when uncommented? Why? What value does `list.get(1)` return, and how could you explicitly stub it?

### Question 2

How do Mockito argument matchers work? Use `letsMockListGetWithAny` to explain why one stub applies to several integer arguments.

### Question 3

Describe the interactions in `TodoBusinessImplMockitoTest`. Clearly identify:

- the class under test;
- the mocked dependency;
- the stubbed behavior;
- the method call being tested; and
- the assertion or verification that determines whether the test passes.


