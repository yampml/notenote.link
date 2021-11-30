---
title: Spring AOP
tags: [[Spring]], [[AOP]]
season: winter
---

## Advice Types
- Before advice: run before the method
- After returning advice: run after the method (success execution)
- After throwing advice: run after the method (if exception thrown)
- After finally advice: run after the method (finally)
- Around advice: run before and after method

### @Before Advice
- Need to manually add AspectJ library?
	- Spring AOP only uses some of the AspectJ annotations
	- Spring AOP only uses some of the AspectJ classes
- Java config class
```java
@Configuration
@EnableAspectJAutoProxy
@ComponentScan("package...")
public class DemoConfig {}
```


- Main App -> AOP Proxy ---> Logging Aspect/ Security Aspect -> Target Object
```java
@Before
public void doSomething() {
	//...
}
```

- Most common use cases:
	- logging, security, transactions
	- audit logging: who, what, when, where
	- API management
		- how many times has a method benn called
		- analytics: what are peak times? average load? who is top user?

```java
@Aspect
@Component
public class DemoLoggingAspect {
	@Before("execution(public void addAccount())")
	public void beforeAddAcountAdvice() {
	
	}
}
```

- Pointcut expression: run this code BEFORE - target object method: "public void addAccount()"

### Pointcut expressions - Match methods and Return types

- Spring AOP uses AspectJ's pointcut expression language
- Match on method name and return types:
	- execution(modifiers-pattern? return-type-pattern declaring-type-pattern? method-name-pattern(param-pattern) throws-pattern?)
		- modifiers-pattern
		- return-type-pattern
		- declaring-type-pattern
		- method-name-pattern(param-patten)
		- throws-pattern
- Examples:
	- Match only addAccount() method in AccountDAO class
		- @Before("execution(public void packageabc.AccountDAO.addAccount())")
	- Match any addAccount() method in any class
		- @Before("execution(public void addAccount())")
	- Match methods starting with add in any class
		- @Before("execution(public void add*())")
	- Can use wildcard against return types, method name,...
		- @Before("execution(* processSomething*())")

### Pointcut expressions - Match method parameter types
- For param-pattern:
	- () - matches a method with no argument
	- (*) matches a method with one argument of any type
	- (..) matches a method with 0 or more arguments of any type

- Examples:
	- Match addAccount methods with no arguments
		- @Before("execution(* addAccount())")
	- Match addAcount methods that have Account param
		- @Before("execution(* addAccount(packageabc.Account))")
	- Match addAccount methods with any number of arguments
		- @Before("execution(* addAccount(..)")

- Match all methods in a package
	- @Before("execution(* com.package.*.*(..))")

### AOP Pointcut Declarations
- How to reuse a same pointcut expression on multiple advices
- Solutions
1. Create a pointcut declarations
```java
	@Pointcut("execution(* com.package.*.*(..))")
	private void forSomePackage() {}
```
2. Apply it everywhere!
```java
	@Pointcut("forSomePackage()")
	private void beforeSomeMethod() {}
```

### AOP Pointcut Combination
- How to apply multiple pointcut expressions to single advice?
	- For examples: All methods in a package EXCEPT getter/setter methods...
--->Combine pointcut expressions using logic operators
	-	AND (&&)
	-	OR (||)
	-	NOT (!)
-	Examples: 
	-	@Before("expressionOne() && expressionTwo()")
	-	@Before("expressionOne() || expressionTwo()")
	-	@Before("expressionOne && !expressionTwo()")
-	All methods in a package EXCEPT getter/setter methods
	-	@Before(* com.package.*.*(..) && !* com.package.*.get*() && !* com.package.*.set*(..)) ???? bad
	-	Good:

```java
@Before("* com.package.*.*(..)")
private void forAllMethod()

@Before("* com.package.*.get*(..)")
private void forGetter()

@Before("* com.package.*.set*(..)")
private void forSetter()

@Before("forAllMethod() && !(forGetter() && forSetter())")
private void forAllExceptGetSet()
```


