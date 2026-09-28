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

**Abstract Syntax Trees**
