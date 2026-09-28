date: 24-09-2026
time: 22:14
topic: Abstract Syntax
tags:

**L-arith**
Used to illustrate concepts.
e.g. 1 + 2 ---> 3

**Concrete vs Abstract Syntax**
- **Concrete syntax** is used in front-end. It deals with strings eventually executing as a program. Specified through **context-free grammars**
- **Abstract syntax** is used in middle and back-end. Essential constructs of program - *internal representation* of a program. Specified using Backus-Naur Form

**Context-free Grammars**
![[Pasted image 20260928113003.png]]
Non-terminals - E , F
Terminals/Tokens - TIMES , PLUS , ->
- generates strings from interpreting tokens, if can't be generates then not valid (?)

**BNF Grammars**
- used to define abstract syntax trees from different expressions
- parentheses are not part of the rules but are used for readability
 ![[Pasted image 20260928113312.png]]
 ::= consists of

# Abstract Syntax Trees

- BNF grammar defines a collection of syntax trees
![[Pasted image 20260928114823.png]]

#### ASTs in Java
```
abstract class Expr {}
class Num extends Expr {
     public int n;
     Num(int \_n) {
         n = \_n;
     }
 }
```
- can use abstract classes to define a base expression, which all expressions would use
- ASTs creates a *class hierarchy*
- we can define our binary node (is used to refer to a recursive node in BNF, where 2 subtrees - 2 child nodes - are referenced to)
---
```
class Plus extends Expr {
	public Expr e1;
	public Expr e2;
	Plus(Expr _e1, Expr _e2) {
		e1 = _e1;
		e2 = _e2;
	}
}

class Times extends Expr {...}
```
---
- traverse the AST by adding a method to each class
- e.g. for a method returning size():
---
```
abstract class Expr {
	abstract public int size();
}

class Num extends Expr { ...
	public int size() {
		return 1;  // num has a fixed tree size of 1 node
	}
}

class Plus extends Expr { ...
	public int size() {
		return e1.size() + e2.size() + 1;
	}
}

class Times extends Expr { ... // similar }
```
---
#### ASTs in Python
- similar but shorter if you use *dataclass* syntax
- can define an abstract class by defining a class and using 'pass'

```
class Expr:
	pass
	
@dataclass
class Num(Expr):
	n: int
	def size(self): return 1
	
@dataclass
class Plus(Expr):
	e1: Expr
	e2: Expr
	def size(self):
		return self.e1.size() + self.e2.size() + 1
```
#### ASTs in Haskell
- ASTs are defined using *datatypes* e.g.
```
data Expr = Num Interger
			| Plus Expr Expr
			| Times Expr Expr
```
- can write functions which go through all the cases called *pattern matching*
```
size :: Expr -> Integer
size (Num n) = 1
size (Plus e1 e2) =
	(size e1) + (size e2) + 1
size (Times e1 e2) =
	(size e1) + (size e2) + 1
```

#### ASTs in Scala
