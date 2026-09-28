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
Terminals/Tokens - TIMES , PLUS , ->, NUM
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
     Num(int _n) {
         n = _n;
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
> [!NOTE] Creating AST
> ```
> new Plus(new Num(2), new Num(2))
> ```
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
> [!NOTE] Creating AST
> ```
> Plus(Num(2), Num(2))
> ```
#### ASTs in Haskell
- ASTs are defined using *datatypes* e.g.
```
data Expr = Num Integer
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
> [!NOTE] Creating AST
> ```
> Plus(Num(2)) (Num(2))
> ```
#### ASTs in Scala
- ASTs are defined using *class cases*, it is like a hybrid of the other 2 methods
- start off like Java, using abstract class and extending from the base abstract class Expr using *case class*, which is like pattern matching but for classes
```
abstract class Expr
case class Num(n: Integer) extends Expr
case class Plus(e1: Expr, e2: Expr) extends Expr
case class Times(e1: Expr, e2: Expr) extends Expr
```

then use pattern matching when writing functions, like in Haskell
```
def size (e: Expr): Int = e match {
	case Num(n) => 1
	case Plus(e1, e2) =>
		size(e1) + size(e2) + 1
	case Times(e1, e2) =>
		size(e1) + size(e2) + 1
}
```

> [!NOTE] Creating AST
> ```
> new Plus(new Num(2), new Num(2))
> ```
> OR (without the 'new')
> ```
> Plus(Num(2), Num(2))
> ```

#### Precedence, Parentheses and Parsimony
- Infix notation and precedence are useful but can become quite complex
- we can use *Symbolic Expressions* (S-Expressions) to make the connection between human notation and ASTs smaller - their concrete syntax is close to abstract syntax
![[Pasted image 20260928132125.png]]
- you either have *atoms*, which are literals (string, number, symbols etc.), or *parentheses*, followed by an atom, and then a sequence of S-Expressions
- 1 + 2 ---> (+ 1 2)
- 1 + 2 * 3 ---> (+ 1 (* 2 3))
- (1 + 2) * 3 ---> (* (+ 1 2) 3)

