---
layout: single
title: "Clean Code"
date: 2019-04-22 21:06
tags: Software Coding
---

## Recommended Books
* Working Efficiently With Legacy Code
* User Stories Applied _For Agile Software Development_ by `Mike Cohn`

## SOLID principle
* [Single responsibility principle](https://en.wikipedia.org/wiki/Single_responsibility_principle)
	* a class should have only a single responsibility (i.e. changes to only one part of the software's specification should be able to affect the specification of the class)
* [Open/closed principle](https://en.wikipedia.org/wiki/Open/closed_principle)
	* software entities (classes, modules, functions, etc.) should be open for extension, but closed for modification
* [Liskov substitution principle](https://en.wikipedia.org/wiki/Liskov_substitution_principle)
	* objects in a program should be replaceable with instances of their subtypes without altering the correctness of that program.
	* See also [design by contract](https://en.wikipedia.org/wiki/Design_by_contract)
* [Interface segregation principle](https://en.wikipedia.org/wiki/Interface_segregation_principle)
* [Dependency inversion principle](https://en.wikipedia.org/wiki/Dependency_inversion_principle)

## SOLID

![](/assets/images/clean-code/SOLID.jpg)


## Three laws of TDD:

1. Write failing test first
2. Write only enough test to fail
3. Write only enough code to pass

If the test gets more specific, the code gets more generic.

## Transformation List

* Null
* Null to constant
* Constant to variable
* Add computation
* Split flow
* Variable to array
* Array to container
* If to while
* Recurse
* Iterate
* Assign
* Add case
