---
title: 'Complete JavaScript Course: Basics'
date: 2017-04-02 08:00:19
tags:
- 学习笔记
- tech
- JavaScript
---

## 1. What is JavaScript?
JavaScript is a lightweight, cross-platform, object-oriented computer programming language
- JavaScript is one of the three core technologies of web development
- JavaScript is most commonly used as a part of webpages
- Today, JavaScript can be used in different places:
	- Client-side: JavaScript was traditionally only used in the browser
	- Server-side: Thanks to node.js, we can use JavaScript on the server as well
- JavaScript is what made modern web development possible:
	- Dynamic effects and interactivity;
	- Modern web applications that we can interact with.

## 2. JavaScript Basics
### 2.1. Declare a variable:
```javaScript
var name = 'John';
console.log(name);

var lastName = "Smith"; //Both single quotes and double quotes work, but need to keep consistent.
console.log(lastName);

var age = 26;
console.log(age);

var fullAge = true;
console.log(fullAge);

```

### 2.2. Primitive Javascript Data Types, Variable Mutation and Type coercion
- **Number**: Floating point numbers, for decimals and integers
- **String**: Sequence of characters, used for text.
- **Boolean**: Logical data type that can only be true of false
- **Undefined**: Data type of a variable which doe not have a value yet.
- **Null**: Also means ‘non-existent’.

`JavaScript has dynamic typing`
We don’t need to define the variable type, Javascript will figure it out by itself.

**Variable Mutation & Type coercion**
```javaScript
var name = 'Danny';
var age = 27;
console.log(name + age); //Type coercion: String + Number = String
age = "twenty seven" //Variable Mutation: the data type can be changed for the same virable.
consol.log(name + age);
```

**Prompt & Alert**
```javaScript
var lastName = prompt('What is the last name?'); //Allow user to type in.
alert('The last name is ' + lastName);
```

### 2.3. Operators
例子都很简单，在JavaScript中各种运算符的优先顺序可参考：
- [Operator precedence](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Operators/Operator_Precedence)

### 2.4. If else statements

### 2.5. == vs ===
`==`: does type coercion
`===`: does not do type coercion

```javaScript
	if (23 == '23') {
		//Result is true, javaScript transform 23 to string and compare with '23'
	}

	if (23 === '23') {
		//Result is false, to avoid bugs, it's more recommended to use ===
	}

```

### 2.6. Boolean Logic and Switch Statements:
Too basic, and the same as Java

### 2.7. Functions

```javaScript
function calculateAge(yearOfBirth) { //Function with return value.
	var age = 2016 - yearOfBirth;
	return age;
}

var ageJohn = calculateAge(1990);
console.log(ageJohn);

function yearsUntilRetirement(name, yearOfBirth) { //Function without return value.
	var age = calculateAge(yearOfBirth);
	var retirement = 65 - age;
	console.log(name + 'retires in ' + retirement + 'years.');
}

yearsUntilRetirement('John', 1990);
```

### 2.8. Statements and Expressions
```javaScript
//Function Statement
function someFun(par) {
	//code
}

//Function Expression
var someFun = function(par) {
	//code
}
```

Difference:
- Function expression produces a value and outcome
- Statement just performs an action

### 2.9. Arrays

```javaScript
var names = ['John', 'Jane', 'Mark'];
var years = new Array(1990, 1969, 1948);

console.log(names[0]);
names[1] = 'Ben';
console.log(names);

var john = ['John', 'Smith', 1990, 'designer', false];

john.push('blue'); //Add an element to the end
john.unshift('Mr.'); //Add an element to the beginning
john.pop(); //Remove an element from the end
john.shift(); //Remove an element from the beginning
john.indexOf('Smith'); //Return the index of an element
console.log(john);

if (john.indexOf('teacher') === -1) {
	console.log('John is NOT a teacher.');
}

```

### 2.10. Objects and Properties

```javaScript
var john = {
		name: 'John',
		lastName: 'Smith',
		yearOfBirth: 1990,
		job: 'teacher',
		isMarried: false
};

console.log(john); //Print out all properties
console.log(john.lastName); // Print out specific property
console.log(john['lastName']); // Print out specific property

var xyz = 'job';
console.log(john[xyz]);

john.lastName = 'Miller';
john['job'] = 'programmer';
console.log(john);

//A different way to create object
var jane = new Object();
jane.name = 'Jane';
jane.lastName = 'Smith';
jane['yearOfBirth'] = 1969;
jane['job'] = 'retired';
jane['isMarried'] = true;

console.log(jane);
```

### 2.11. Objects and Methods
```javaScript

var john = {
		name: 'John',
		lastName: 'Smith',
		yearOfBirth: 1990,
		job: 'teacher',
		isMarried: false,
		family: ['Jane', 'Mark', 'Bob'],
		/*
		calculateAge: function() { //Function Expression
				return 2016 - this.yearOfBirth;
		} */
		calculateAge: function() { //Function Expression
				return 2016 - this.yearOfBirth;
		}
};

console.log(john.family);
console.log(john.family[2]);
//console.log(john.calculateAge(1990));
console.log(john.calculateAge());

var age = john.calculateAge();
john.age = age;

console.log(john);

//v2.0
var john = {
		name: 'John',
		lastName: 'Smith',
		yearOfBirth: 1990,
		job: 'teacher',
		isMarried: false,
		family: ['Jane', 'Mark', 'Bob'],
		/*
		calculateAge: function() { //Function Expression
				return 2016 - this.yearOfBirth;
		} */
		calculateAge: function() { //Function Expression
				this.age = 2016 - this.yearOfBirth;
		}
};

john.calculateAge（）；
console.log(john);

```

### 2.12. Loops and Iteration

```javaScript
//for loops
for (var i = 0; i < 10; i++) {
	console.log(i);
}

var names = ['John', 'Jane', 'Mary', 'Mark', 'Bob'];
for (var i = 0; i < names.length; i++) {
	console.log(names[i]);
}

for (var i = names.length - 1; i >=0 ; i—) {
	console.log(names[i]);
}

var i = 0;
while (i < names.length) {
	console.log(names[i]);
	i++;
}

for (var i = 0; i < 5; i++) {
	console.log(i);
	if (i === 3) {
		break;
	}
}

for (var i = 0; i < 5; i++) {
	if (i === 3) {
		continue;
	}
	console.log(i);
}

```

## 3. History and Versions
### 3.1. A Very Short History of JavaScript
- **1996**: Changed from LiveScript to JavaScript to attract Java developers. **JavaScript has almost nothing to do with Java**.
- **1997**: ECMAScript 1 became the fist version of the JavaScript language standard:
	- ECMAScript: The language standard;
	- JavaScript: The language in practice.
- **2009**: ECMAScript 5 (ES5) was released with logs of new features.
- **2015**: ECMAScript 2015 (ES2015) was released: **the biggest update ever**.
- **2016**: ECMAScript 2016 (ES2016) was released with minor changes only.

### 3.2. JavaScript Today
- `ES5`
	- Fully supported in all modern browsers;
	- Ready to be used today (2016).

- `ES6/ES2015`
	- Only partial supported in modern browsers, no support in older browsers;
	- Can’t use it in production today (2016).

- `ES2016`
	- Almost no support in modern browsers;
	- Can’t use it in production today (2016).

### 3.3. Why We’re Using ES5 in This Course
- ECMAScript 2015 still has very incomplete browser support today.
- Almost all tutorials and code you find on the web today is till in ES5
- When working on older codebases, these will be written in ES5.
- It’s easier to learn ES5 and then update to ES6/ES2015.
