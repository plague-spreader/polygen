# Polygen

The original author is Alvise Spanò


This was   **N O T**   written by me, I just downloaded the source code from
[here](https://polygen.org/it/casa) and ported it to OCaml 5.3.0

Also, I know nothing about OCaml. The porting was done by just pure
guess-working and Google searches.

## Description

This program can generate strings given a type-2 grammar.

The grammar meta-language are written in a slightly more expressive version of
EBNF (Extended Backus-Naur Form).
Refer to the manuals in the `manual` directory (currently only the Italian
version is available) or to the `Quick grammar description` below.

In the `grm` directory there are examples; all of these are
parodying habits, stereotypes and trends (of Italy in the 2000s).

### How to parody (extracted from polygen website)
A parody is constructed by focusing on one particular topic (a funny one) and
then by extracting and abstracting as much rules and patterns (in a formal
grammar fashion).

Polygen will then reproduce it by randomly creating strings according to the
input grammar. 

Randomicity is perfect for this purpose since it is unpredictable and does not
follow sentence's semantics.

## Usage

`polygen` -> will print an help message

`polygen <grammar file>` -> will generate a grammar starting from the `S`
non-terminal symbol

`polygen -S <SYM> <grammar file>` -> will generate a grammar starting from the
`<SYM>` non-terminal symbol

## Quick grammar description

Terminal symbols are any contiguous (i.e. without any spaces between) sequence
of characters starting with a lower case letter or any sequence of characters
enclosed by double quotes.

Non-terminal symbols are any contiguous sequence of characters starting with a
upper case letter.

The `::=` operator is defines the production for the non-terminal symbol in the
left-hand side (denoted with LHS in short).

The pipe character (`|`) is separating the definition of the production rule in
the right-hand side (denoted with RHS in short).

You can "save" the definition of a non-terminal symbol by using the `:=`
operator; you have to enclose the whole definition in round brackets.

A sequence of two (or more) symbols (either terminal or non-terminal) are
separated by space. Using the caret (`^`) operator it will remove the space.

The underscore (`_`) character represents an epsilon production. Basically it
is an empty string.

You can use the backslack (`\`) character to escape the following characters
(it means that you remove the semantics associated with the following character
and it will be printed as it is)

A production rule MUST end with a semicolon (`;`)

### Example 1:
    S ::= Name VerbObject;
    Name ::= "John" | "Richard" | "STOCAZZO";
    Verb ::= "eats" Eatable | "drinks" Drinkable | "goes" Place;
    Eatable ::= "an apple" | "a whole watermelon";
    Drinkable ::= "a glass of water";
    Place ::= "to Fanculo" | "in the Wisconsin";

### Example 2:
    S ::= (N := Name; N says "\"hello\"." N goes to the bathroom);
    Name ::= "John" | "Richard" | "STOCAZZO";
