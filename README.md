# Coby

This is the demo repository for submission 34, "Formalizing Relational Block Descriptions for Hardware Design".

## Ruby Cheat Sheet

A Ruby cheat sheet `cheatsheet.pdf` is provided to help understand the language better. It is written in mathematical language and is comparable with Coq source code.

The core of combinating Ruby blocks are two compositions. Two blocks $R; S$ are connected by series composition:

$a(R;S)b \iff \exists c.\, a\,R\,c \land c\,S\,b.$

Two blocks $[R, S]$ are in parallel by parallel composition:

$\langle a,c\rangle [R,S] \langle b,d\rangle \iff a\, R\, c \land b\, S\, d.$

Their Coq definitions follow a similiar logic.

```
Definition series {A B C} 
  (R: rel A B) (S: rel B C): 
  rel A C := 
  fun i j => exists2 k, R i k & S k j.
```
```
Definition parallel {A B C D}
  (R: rel A C) (S: rel B D): 
  rel (A*B) (C*D) :=
  fun i j => R (fst i) (fst j) /\ S (snd i) (snd j).
```

## Coq Source Code

Coq source code is tested with Coq 8.16. It covers the examples in the submission and most examples in the Ruby cheat sheet. All examples should be self-explanatory based on their definitions and verification.