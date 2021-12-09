---
title: Functional Programming in Java
tags: markdown, functional 
season: summer
---

## 1. Functional Interface
- A functional interface is an interface that contains only one abstract method.

```
@FunctionalInterface
public interface MyFuncInterface {
	public void myMethod();
	// adding another method will result in error
}
```

- How lambda work under the hood:
	-	invokedynamic since jvm7
	-	Lambdas: Type Inference and Invokedynamic

-	Imperative vs Declarative
	-	Functional Programming is a **subset** of Declarative Programming
	-	Declarative is more readable.
	-	Declarative is much safer in multithreaded environments.

## 2. Practices
### Imperative function
-	Access Modifier (public, private, protected,...)
-	Return Type
-	Name of the Function
-	Parameters List and Parameters Type
-	Method Body
-	Return statement

### Lambda
- A list of params
- An arrow -> which separate the list of parameters from the body of the lambda function
- The body of the lambda

## 3. Predefined Functional Interfaces
-	Predicate: to test a condition
	-	Predicate<T> : T -> boolean
-	Consumer: consumer to consume something and return back nothing
	- Consumer<T> : T -> void
-	Function: takes something and return something
	- Function<T, R> : T -> R
-	Supplier: accept nothing, but return something
	- Supplier<T> :  () -> T
- UnaryOperator<T> : T -> T
	
- BinaryOperator<T> : (T, T) -> T
- BiPredicate<L, R> : (L, R) -> boolean
- BiConsumer<T, U> : (T, U) -> void
- BiFunction<T, U, R> : (T, U) -> R
	




