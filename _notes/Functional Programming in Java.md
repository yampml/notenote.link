---
title: Functional Programming in Java
tags: functional 
season: summer
---

## 1. Functional Interface
- A functional interface is an interface that contains only one abstract method.

```java
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
	
## 4. Method Reference vs Constructor Reference

- Method Reference
	- Constructor: ClassName::new
	- static method: ClassName::staticMethodName
	- instance method of an existing object: object::instanceMethodName
	- instance method of an abitrary object: ClassName::instanceMethodName
	
## 5. Functional Programming

- Think about a pure mathematical function.
	- A pure mathematical function's job would only be to perform calculation on the basis of provided algorithm and add nothing more than that.
	- It should not have any effect on the outer environment.
- Declarative: What to solve rather then how to solve.

- Concepts: 
	- Functions as first class citizens
	- Pure functions
	- Higher order functions
	- No side effects
	- Referencial Transparency
	
### 5.1 Function as first class citizens
`int result = myFunction(int a);`
-> Functional Programming:
`Function aFunc = myFunction(Function func);`

### 5.2 No side effects - Pure functions
- The output of the function depends only on 
	(a) its input parameters
	(b) its internal algorithm
- A pure function has no Side Effects.
+ Side Effects: can be anything a method does beside computing and returning the result.

### 5.3 Higher order functions
- `higerOrderFunction(Function one, Function two)`

### 5.4 Referencial Transparency
- Referencial transparency is A property of a function, variable or expression whereby the expression can be replaced by its (evaluated) value without affecting the behaviour of the program.

### 5.5 Functional Programming Techniques
- Function Chaining
	- Is a technique where we chain functions, each method returns an object allowing the calls to be chained together in a single statement without requiring variables to store the intermediate results.
	- aka: obj.call1().call2().call3()
	
- Functional Composition
	- Composing function is different from chaining functions: composing reverse direction to the direction we used when chaining
- Closures
- Currying
- Lazy Evaluation
- Tail Call Optimization

	Design APIs In functional way: Function Chaining + Functional Composition
	

## 6. Streams
- The Stream takes data from a source
	- Do all the processing
		- Return the data into the container the user wants or just consumes the data.
	
```java
List<Book> books = new ArrayList<>();
List<Book> popularBooks = new ArrayList<>();

for(Book book : books) {
	if(book.getGenre().equalsIgnoreCase("Horror") && book.getRating() > 3) {
		popularHorrorBooks.add(book);
	}
}
```
	
- After java 8 with stream:
```java
books.stream()
	.filter(book -> book.getGenre().equalsIgnoreCase("Horror"))
	.filter(book -> book.getRating() > 3)
	.collect(Collectors.toList());
```