# Tutorial #3: Mocking
## Introduction:
In this tutorial, you will learn how to learn what Mocking is and how to mock some
objects.

## Definition:
Mocking is creating objects that simulate the behavior of real objects. An object that you
want to test may have dependencies on other complex objects. In unit testing, we use
mocking to isolate the behavior of the objects you want to test by replacing the other objects
by mocks, simulating the behavior of the real objects.
## Goals
   - Classes are not isolated. They may use services and methods that are from other
       classes. We want to mock the behavior of these dependencies.

## Mechanism:
The mechanism of mocking is to mock the services and methods from other classes and
simulate the real behavior of them using some mocking frameworks and use that mocked
methods and services to do unit testing in isolation. This is where Mocking frameworks come
into play.

## Tools:
   - Frameworks available for mocking in unit testing include PowerMock, EasyMock, and
        Mockito.
In this tutorial, we will use the Mockito framework for mocking.
The documentation for the Mockito framework can be found here:
https://javadoc.io/static/org.mockito/mockito-core/3.2.4/org/mockito/Mockito.html

## Mockito - Features:
   - Mockito is a proxy based framework

A proxy is just an object which will be used instead of the original object. If a method of the
proxy object is called than the proxy object can decide what it will do with this call:

        - delegate it to the original object

        - handles the call itself

A proxy doesn’t require an instance of an interface/class if the proxy handles all method
invocations itself.

## Environment Requirements:
Please make sure that you have Maven and Java installed on your computer.
   - OS: macOS 10.16
   - Eclipse: version 2021-6
   - Java: version 1.8

   - Maven: version 3.6.3

Note: Only the above environment is tested by us, not sure if other versions work well.

## Experiment:
Please make sure that you have Maven and Java installed on your computer.

## Part A (Integrate Mockito and JUnit testing tool into an example project)

press Next

press Next (make sure to select Create a simple project)

Fill in the information and Press Finish

Open pom.xml

Add in before </project> to download the dependencies for JUnit and Mockito framework:

```xml
   <dependencies>
<dependency>
  <groupId>junit</groupId>
  <artifactId>junit</artifactId>
  <version>4.12</version>
  <scope>test</scope>
</dependency>
<dependency>
  <groupId>org.mockito</groupId>
  <artifactId>mockito-all</artifactId>
  <version>1.10.19</version>
  <scope>test</scope>
</dependency>
   </dependencies>
```

Check that JUnit is working - The test actually does not contain any Mockito functions yet:

## Part B: (Paste in your first basic Mockito test cases)
Create a JUnit test case named ListTestTest
You can paste the code from ListTestTest.java in Tutorial3.zip.

When run, this should be shown:

For each of the four unit tests, you can see the line List list = mock(List.class);

The mock function takes in a parameter of type Object.class to mock

To make letsMockListSizeWithMultipleReturnValues() pass, add this line after the
commented line:

when(list.size()).thenReturn(10, 20);

Now run the tests again and it should pass.

By default, for all methods that return a value, a mock will return either null, a
primitive/primitive wrapper value, or an empty collection, as appropriate. For example 0 for
an int/Integer and false for a boolean/Boolean.

Once stubbed, the method will always return a stubbed value, regardless of how many times
it is called, unless overridden by specifying another value through another stub.

The last stubbing is more important - when you stubbed the same method with the same
arguments many times. Other words: the order of stubbing matters but it is only
meaningful rarely, e.g. when stubbing exactly the same method calls or sometimes when
argument matchers are used, etc.

## Part C: (Mocking a class implementation)
Now that we have mocked the List class from Java, we will see how mocking a dependency
works. In real life, rather than mocking a List object, we would have instances of an actual
one. You can find the following Java files in Tutorial3.zip.
TodoService.java interface
TodoBusinessImplMockitoTest.java test case
TodoBusinessImpl.java class
After you finish all the experiment parts (part A to part C), you need to answer the
corresponding questions in the following report and provide appropriate screenshots and / or
source files to support your answers.

Please submit it as a PDF file on moodle with the file name of
‘Tutorial3_yourname_yourstudentID.pdf’.

Last but not least, plagiarism is prohibited. Have fun!

## Tutorial #3 report
                                       Student number:
                                        Student name:

Question 1 [2%]: For @Test public void letsMockListGet(), does the commented line
// assertNull(list.get(1)); pass or fail when uncommented? Why? If it fails, how do we make it
pass? What is the value of list.get(1)?

Question 2 [2%]: Mockito has something called “ArgumentMatchers”. How do they work?
There is an example in the test case @Test public void letsMockListGetWithAny(), which
passes when run. How does this work?

Question 3 [2%]: Copy the three files above into the same test directory as Part C
Observe the three files and run the unit tests in TodoBusinessImplMockitoTest.java. Describe the
interactions.
