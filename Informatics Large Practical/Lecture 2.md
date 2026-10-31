date: 28-09-2026
time: 17:00
topic: Lambdas, Optional, Generics, Collections, Streams, DTOs, MapStruct and ObjectMapper
tags:

# Lambda
- a short block of code which takes 0 or more parameters and returns a value
- format:
	- () -> *expression*
	- *parameter* -> *expression*
	- (*parameter1, parameter2*) -> *expression*

```
Predicate<Order> isExpensive =
	order -> order.total().compareto(new BigDecimal("100")) > 0;
// returns True if the compareto method returns 1 for > 100
// returns False if it returns -1 for smaller than 100
```

- lambdas are instances of *functional interfaces*
	- *functional interfaces* - an interface containing a single abstract method
- to store a lambda in a variable, the type of the variable must be a functional interface

```
public interface Printable{
	void print(); // Printable is a functional interface
}

public class Lambdas{
	static void printThing(Printable thing){
		thing.print(); // calls the print method from Printable
	}
}

public class Demo{
	Lambdas l = New Lambdas();
	l.printThing(() -> System.out.println("Hello"));
}
```

#### Method Reference Syntax
An even more shorthand way for lambdas
![[Pasted image 20261015165436.png|563]]
- no parameters so no brackets

# Optionals<\T>
- helps to catch exceptions and prevent runtime exceptions
	- compile time exceptions are better than runtime ones for ur programs

```
public Optional<Order> findbyId(String orderId) {
	return Optional.ofNullable(orderById.get(orderId));  // of(..) method also exists but will throw an exception if .. is null
}

Order order = repository.findById("1111-1111")
	.orElseThrow(() -> new IllegalArgumentException("Order not found"));  // custom error handling
System.out.println(order.getCustomer());  // will never result in NullPointerException
```
- the findById method uses Optional's static method .ofNullable() so that the risk of receiving a Null Exception is there
- if Null happens it will be caught and custom exception message will be displayed instead
- client will then have to handle the Null order

**32:58 lecture**