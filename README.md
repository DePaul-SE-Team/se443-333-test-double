# Tutorial #3: Mocking

## Introduction
In this tutorial, you will learn how to learn what Mocking is and how to mock some
objects.

## Definition
Mocking is creating objects that simulate the behavior of real objects. An object that you
want to test may have dependencies on other complex objects. In unit testing, we use
mocking to isolate the behavior of the objects you want to test by replacing the other objects
by mocks, simulating the behavior of the real objects.

## Goals

- Classes are not isolated. They may use services and methods that are from other
classes. We want to mock the behavior of these dependencies.

## Mechanism
The mechanism of mocking is to mock the services and methods from other classes and
simulate the real behavior of them using some mocking frameworks and use that mocked
methods and services to do unit testing in isolation. This is where Mocking frameworks come
into play.

## Tools

- Frameworks available for mocking in unit testing include PowerMock, EasyMock, and
Mockito.
In this tutorial, we will use the Mockito framework for mocking.
The documentation for the Mockito framework can be found here:
<https://javadoc.io/static/org.mockito/mockito-core/3.2.4/org/mockito/Mockito.html>

## Mockito - Features

- Mockito is a proxy based framework

A proxy is just an object which will be used instead of the original object. If a method of the
proxy object is called than the proxy object can decide what it will do with this call:

- delegate it to the original object
- handles the call itself

A proxy doesn’t require an instance of an interface/class if the proxy handles all method
invocations itself.

## Experiment

### Part B — Basic Mockito tests

Open the provided `ListTestTest.java`. Each of its four tests creates a mock of the Java `List` interface. Start with `letsMockListSize()` to see how a test configures the mock to return a particular value when a method is called.

#### Stub consecutive return values

In `letsMockListSizeWithMultipleReturnValues()`, replace the TODO with one Mockito statement. Configure the first call to `list.size()` to return `10` and the second call to return `20`. Keep the existing assertions and run the test again.

#### Explore unstubbed calls and argument matchers

In `letsMockListGet()`, uncomment the assertion for `list.get(1)`, run the test, and record what happens for Question 1. Then run `letsMockListGetWithAny()` and examine how the existing test uses an argument matcher.

By default, a mock returns a value appropriate to the return type when a call has no matching stub. Examples include `0` for `int` or `Integer`, `false` for `boolean` or `Boolean`, and empty collections for supported collection types.

A stub with a single return value keeps returning that value on matching calls. A stub can also specify different values for consecutive calls. When the same method call matches multiple stubs, the most recently defined matching stub takes precedence.

### Part C — Mocking a dependency

In the provided project, open `TodoService.java`, `TodoBusinessImpl.java`, and `TodoBusinessImplMockitoTest.java`. Run `TodoBusinessImplMockitoTest` and trace how the test configures a mock service, passes it to the business class, and checks the result. Use what you observe to answer Question 3.

## Now answer questions below:

### Question 1 [2%]

For `letsMockListGet()`, does the assertion `assertNull(list.get(1));` pass or fail when uncommented? Why? If it fails, how would you make it pass? What is the value of `list.get(1)`?

### Question 2 [2%]

How do Mockito argument matchers work? Use the existing test `letsMockListGetWithAny()` to explain why its assertions pass.

### Question 3 [2%]

Review `TodoService.java`, `TodoBusinessImpl.java`, and `TodoBusinessImplMockitoTest.java` in the starter project. Run the test in `TodoBusinessImplMockitoTest.java` and describe how the three files interact.
