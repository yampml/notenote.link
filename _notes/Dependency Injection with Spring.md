---
title: Dependency Injection with Spring
tags: DI
season: winter
---

## SOLID Principles of OOP
### Single Responsibility Principle
- Every class should have a single responsibility
- There should never be more than one reason for a class to change
- Your classes should be small
- Avoid "god" classes
- Split big classes into smaller one
### Open closed Principle
- Your classes should be open for extension
- But closed for modification
- You should be able to extend a classes behavior without modifying it
- Use private variables with getters and setters ONLY when you need them
- Use abstract base classes
### Liskov Substitution Principle
- Objects in a program would be replaceable with instances of their subtypes without altering the correctness of the program.
- Violations will often fail the "Is a" test
- A Square "Is a" Rectangle
### Interface Segregation Principle
- Make fine grained interfaces that are client specific
- Many client specific interfaces are better than one "general purpose"
- Keep your components focused and minimize dependencies between them
- Notice relationship to the Single Responsibility Principle?
	- ie avoid "god" interface
### Dependency Inversion Principle
- Abstractions should not depend upon details
- Details should depend upon abstractions
- Important that higher level and lower level objects depend on the same abstract interaction
- This is not the same as Dependency Injection - which is how objects obtain dependent objects


## The Spring Context
```java
@Controller
public class MyController() {
	public String sayHello() {
		return "Hellooooo";
	}
}
```

```java
@SpringBootApplication
public class DemoApplication {
	ApplicationContext ctx = SpringApplication.run(DemoApplication.class, args);
	MyController myController = (MyController) ctx.getBean("myController");
	System.out.println(myController.sayHello());
}
```

```
MyController myController = (MyController) ctx.getBean("myController");
```
- This is an Inversion of Controler example. Spring Container is managing the construction of the mycontroller object.

## Basics of dependency injection
- Dependency Injection is where a needed dependency is injected by another object.
- The class being injected has no responsibility in instantiating the object being injected.
- Types of Dependency Injections:
	- By class properties - least preferred
	- By Setters
	- By Constructor - Most preferred
- Concrete classes vs Intefaces
	- DI can be done with Concrete Classes or with Interfaces
	- Generally DI with Concrete Classes should be avoided
	- **DI via Interfaces is highly preferred**
		- Allows runtime to decide implementation to inject
		- Follows Interface Segregation Principle of SOLID
		- Also, makes your code more testable
- Inversion of Control
	- Is a technique to allow dependencies to be injected at runtime
	- Dependencies are not predetermined
	- One important characteristics of a framework is that the methods defined by the user to tailor the framework will often be called from within the framework itself, rather than from the user's application code. Inversion of control gives frameworks the power to serve as extensible skeletons. The methods are supplied by the user tailor the generic algorithms defined in the framework for a particular application

- IoC vs DI
	- DI refers much to the composition of your classes
		- ie you compose your classes with DI in mind
	- IoC is the runtime environment of your code
		- ie Spring Framework's IoC container
		- Spring is in control of the injection of dependencies

### Some notes
- Spring no longer required an @Autowired for Constructor DI

