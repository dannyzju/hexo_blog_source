---
title: 'Get Ready for the Future: ES6 / ES2015'
date: 2017-07-07 22:05:07
tags:
- 学习笔记
- tech
- JavaScript
---

## 1. What's new in ES6 / ES2015
### 1.1. JavaScript Today
- ES 5:
	- Fully supported in all modern browsers;
	- Ready to be used today(2016)
- ES6 / ES2015
	- Partial supported in modern browsers, no support in older browsers;
	- Can't use it in production today (2016).
- ES2016, ES2017, ...
	- Almost no support in modern browsers;
	- Can't use it in production today (2016)

### 1.2. New ES6 Features We'll Cover in This Section
- Variable Declarations with let and const
- Blocks and IIFEs
- Strings
- Arrow Functions
- Destructuring
- Arrays
- The Spread Operator
- Rest and Default Parameters
- Maps
- Classes and subclasses
- How to use ES2015 / ES6 today!

[ES6 Compatibility Table](https://kangax.github.io/compat-table/es6)

## 2. Variable Declarations with let and const

```javaScript
// ES5
var name5 = 'Jane Smith';
var age5 = 23;
name5 = 'Jane Miller';
console.log(name5);

// ES6
const name6 = 'Jane Smith';
let age6 = 23;
name6 = 'Jane Miller';
console.log(name6); // will get error.

// ES5
// variables in ES5 are function scoped.
function driverLicence (passedTest) {
	if (passedTest) {
		var firstName = 'John';
		var yearOfBirth = 1990;
	}
	console.log(firstName + ', born in ' + yearOfBirth + ', is now officially allowed to drive a car.');
}
driverLicence (true);

// ES6
// variables in ES6 are block scoped.
function driverLicence (passedTest) {
	if (passedTest) {
		var firstName = 'John';
		var yearOfBirth = 1990;
	}
	console.log(firstName + ', born in ' + yearOfBirth + ', is now officially allowed to drive a car.'); // Will get 'firstName' not defined error.
}
driverLicence (true);

```

```javaScript
//ES5
var i = 23;
for (var i = 0; i < 5; i++) {
	console.log(i);
}
console.log(i);
//it will print: 0, 1, 2, 3, 4, 5

//ES6
let i = 23;
for (let i = 0; i < 5; i++) {
	console.log(i);
}
console.log(i);
//it will print: 0, 1, 2, 3, 4, 23
//It's still due to function scoped vs block scoped
```

## 3. Blocks and IIFEs
```javaScript
Block (IIFE) in ES6
{
	const a = 1;
	let b = 2;
	var c = 3;
}

//console.log(a + b); //Will get error
console.log(c); // works good!


//IIFE in ES5: create block that can not be accesed outside.
(function() {
	var c = 3;
})();

//console.log(c);
```

## 4. Strings in ES6 / ES2015

```javaScript
let firstName = 'john';
let lastName = 'Smith';
const yearOfBirth = 1990;
function calcAge(year) {
	return 2016 - year;
}

// ES5
console.log('This is ' + firstName + ' ' + lastName + '. He was born in ' + yearOfBirth + '. Today, he is ' +  calcAge(yearOfBirth) + ' year old.');

//ES6
console.log('This is ${firstName} ${lastName}. He was born in ${yearOfBirth}. Today he is ${calcAge(yearOfBirth)} years old.');

const n = '${firstName} $ {lastName}';
console.log(n.startsWith('J')); //false
console.log(n.endsWith('Sm')); // false
console.log(n.includes(' ')); // true
console.log('${firstName} '.repeat(5)); //John John John John John

```


## 5. Arrow Functions: Basics

```javaScript
const years = [1990, 1965, 1982, 1937];

//ES5
var ages5 = years.map(function(el){
	return 2016 - el;
});

console.log(ages5) //{26, 51, 34, 79}

//ES6
let ages6 = years.map(el => 2016 - el); //Exact same thing.
console.log(ages6); //{26, 51, 34, 79}

ages6 = years.map((el, index) => 'Age element ${index + 1}: ${2016 - el}.');
console.log(ages6);

ages6 = years.map((el, index) => {
	const now = new Date().getFullYear();
	const age = now - el;
	return 'Age element ${index + 1}: ${2016 - el}.'
	});
console.log(ages6);

```

## 6. Arrow Functions: Lexical 'this' Keyword

```javaScript
//ES5
var box5 = {
	color: 'green',
	position: 1,
	clickMe: function() {
		var self = this;
		document.querySelector('.green').addEventListener('click', function(){
			var str = 'This is box number ' + self.position + ' and it is ' + self.color;
			alert(str);
		});
	}
}

box5.clickMe();

//ES6
var box6 = {
	color: 'green',
	position: 1,
	clickMe: function() {
		document.querySelector('.green').addEventListener('click', () => {
			var str = 'This is box number ' + this.position + ' and it is ' + this.color;
			alert(str);
		});
	}
}

box6.clickMe();


function Person(name) {
	this.name = name;
}

//ES5
Person.prototype.myFriends5 = function(friends) {
	var arr = friends.map(function(el){
		return this.name + ' is friends with ' + el;
	}.bind(this));

	console.log(arr);
}

var friends = ['Bob', 'Jane', 'Mark'];
new Person('John').myFriends5(friends);

//ES6
Person.prototype.myFriends6 = function(friends) {
	var arr = friends.map(el =>
	'$(this.name) is friends with ${el}');
	console.log(arr);
}

new Person('Mike').myFriends6(friends);

```


## 7. Destructuring

```javaScript
//ES5
var john = ['John', 26];
//var name = john[0];
//var age = john[1];

//ES6
const [name, year] = ['John', 26];
console.log(name);
console.log(age);

const obj = {
	firstName: 'John',
	lastName: 'Smith'
};

const obj = {
	firstName: 'John',
	lastName: 'Smith'
};

const {firstName, lastName} = obj;
console.log(firstName);
console.log(lastName);

const {firstName: a, lastName: b} = obj;
console.log(a);
console.log(b);

function calcAgeRetirement(year) {
	const age = new Date().getFullYear() - year;
	return [age, 65 - age];
}

const[age2, retirement] = calcAgeRetirement(1990);
console.log(age2);
console.log(retirement);

```

## 8. Arrays in ES6 / ES2015

```javaScript
const boxes = document.querySelectorAll('.box');

//ES5
var boxesArr5 = Array.prototype.slice.call(boxes);
boxesArr5.forEach(function(cur) {
	cur.style.backgroundColor = 'dodgerblue';
})；

//ES6
const boxesArr6 = Array.from(boxes).forEach(cur => cur.style.backgroundColor = 'dodgerblue')；


//Loop
//ES5
for (var i = 0; i < boxesArr5.length; i++) {
	if (boxesArr5[i].className === 'box blue') {
		continue;
	}
	boxesArr5[i].textContent = 'I changed to blue!';
}

//ES6
for (const cur of boxesArr6) {
	if (cur.className.includes('blue')) {
		continue;
	}
	cur.textContent = 'I changed to blue!';
}

//ES5
var ages = [12, 17, 8, 21, 14, 11];
var full = ages.map(function(cur) {
	return cur >= 18;
});
console.log(full);

console.log(full.indexOf(true));
console.log(ages[full.indexOf(true)]);


//ES6
console.log(ages.findIndex(cur => >= 18));
console.log(ages.find(cur => cur >= 18));

```

## 9. The Spread Operator

```javaScript
function addFourages (a, b, c, d) {
	return a + b + c + d;
}

var sum1 = addFourAges () {18, 30, 12, 21};

console.log(sum1);

//ES5
var ages = [18, 30, 12, 21];
var sum2 = addFourAges.apply(null, ages);
console.log(sum2);

//ES6
const sum3 = addFourAges(...ages); //Spread Operator
console.log(sum3);

const familySmith = ['John', 'Jane', 'Mark'];
const familyMiller = ['Mary', 'Bob', 'Ann'];
const bigFamily = [...familySmith, 'Lily', ...familyMiller];
console.log(bigFamily);

const h = document.querySelector('h1');
const boxes = document.querySelectorAll('.box');
const all = [h, ...boxes];

Array.from(all).forEach(cur => cur.style.color = 'purple');

```

## 10. Rest Parameters

```javaScript
//ES5
function isFullAge5() {
	//console.log(arguments);
	var argsArr = Array.prototype.slice.call(arguments);

	argsArr.forEach(function(cur) {
		console.log((2016 - cur) >= 18);
	});
}

isFullAge5(1990, 1999, 1965);
isFullAge5(1990, 1999, 1965, 2016, 1987);

//ES6
function isFullAge6(...years) {
	years.forEach(cur => console.log((2016 - cur) >= 18));
}

isFullAge6(1990, 1999, 1965, 2016, 1987);

```


```javaScript
//ES5
function isFullAge5(limit) {
	console.log(arguments);
	var argsArr = Array.prototype.slice.call(arguments, 1);
	console.log(argsArr);

	argsArr.forEach(function(cur) {
		console.log((2016 - cur) >= limit);
	});
}

isFullAge5(1990, 1999, 1965);
isFullAge5(1990, 1999, 1965, 2016, 1987);

//ES6
function isFullAge6(limit, ...years) {
	years.forEach(cur => console.log((2016 - cur) >= limit));
}

isFullAge6(16, 1990, 1999, 1965, 2016, 1987);

```

## 11. Default Parameters
```javaScript
//ES5
function SmithPerson(firstName, yerOfBirth, lastName, nationality) {
	lastName === undefined? lastName = 'Smith' : lastName = lastName;
	nationality === undefined ? nationality = 'american' : nationality = nationality;

	this.firstName - firstName;
	this.lastName = lastName;
	this.yearOfBirth = yearOfBirth;
	this.nationality = nationality;
}

var john = new SmithPerson('John', 1990);
var emily = new SmithPerson('Emily', 1983, 'Diaz', 'Spanish');

//ES6
function SmithPerson(firstName, yerOfBirth, lastName = 'Smith', nationality = 'american') {
	this.firstName - firstName;
	this.lastName = lastName;
	this.yearOfBirth = yearOfBirth;
	this.nationality = nationality;
}

var john = new SmithPerson('John', 1990);
var emily = new SmithPerson('Emily', 1983, 'Diaz', 'Spanish');

```

## 12. Maps

```javaScript
const question = new Map();
question.set('question', 'What is the official name of the latest major JavaScript version?');
question.set(1, 'ES5');
question.set(2, 'ES6');
question.set(3, 'ES2015');
question.set(4, 'ES7');
question.set('correct', 3);
question.set(true, 'Correct answer :D');
question.set(false, 'Wong, please try again!');

console.log(question.get('question'));
console.log(question.size);
if (question.has(4)) {
	//question.delete(4);
	console.log('Answer 4 is here!');

}
//question.clear();
question.forEach((value, key) =>
	console.log("This is ${key}, and it's set to ${value}'"));

for (let [key, value] of question.entries()) {
	if (typeof(key) === 'number') {
		console.log('Answer ${key}: ${value}');
	}
}

const ans = parseInt(promt('Write the correct answer'));
console.log(question.get(ans === question.get('correct')));

```


## 13. Classes

```javaScript
//ES5
var Person5 = function(name, yearOfBirth, job) {
	this.name = name;
	this.yearOfBirth = yearOfBirth;
	this.job = job;
}

Person5.prototype.calculateAge =
function() {
	var age = new Date().getFullYear - this.yearOfBirth;
	console.log(age);
}

var john5 = new Person5('John', 1990, 'teacher');

//ES6
class Person6 {
	constructor (name, yearOfBirth, job) {
		this.name = name;
		this.yearOfBirth = yearOfBirth;
		this.job = job;
	}

	calculateAge() {
		var age = new Date().getFullYear - this.yearOfBirth;
		console.log(age);
	}

	static greeting() {
		console.log('Hey there!');
	}
}

const john6 = new Person6('John', 1990, 'teacher');
Person6.greeting();

```

## 14. Classes with Subclasses

![Inheritance In General](https://lh3.googleusercontent.com/FSJzIBGVOv7w9a-8El7jRjEgJ1PX4wDMUakG76CcP-r6phX-BErInbk6RYWbOgEuf7FwPo7rLgJCvScUtGncxitTxNkPvqLG4TDBtFpWaE1w4a9JDJoo9dzPJcZLjCanhCOIPiFYu_nSW4RmiKX9VUGPq1VEt5wWWcuKonAi1ZW5QPWtk39mvF4i903oh7RFhQA8UsAXeg9aNRhIwMb6VPRmPXishUTOUKHkAiGsDMDgKpdkEuFr1inz4BVYPoH70NWNmwHZKX-AMRC_kaN3MA_92hAXwO4216NR0zCdi_BVGmrsJQiDDqrghy3SDre1hUQ91t-j8i-NIKEpmvsLWlD9JrZjp9oLfspRm5YiOKmF4ek_6x_tHLSLn1578RY2UUvR8Vyl2GZOTbPmZNfq9933awEjLEk0P7Jx_e_FTwb3a0qHiOZSqRA1IVQFlrYJkHvE4yiGp05D_KEpEQnJiQWOiWOidaHiEqxjMv8BdJKIwHo4fmV15bxT1jY5X09eMY_CHeSMUDnqHfsPskHAyhwoYQjQ4f77XWW7jbmq4J0mLbQxbIYsv5hhOl8rw3Y39BT3G8HmbZXfGKv0ZaCFnHq4hHQQkyRdQIDv_AoknX_Fob4W8_adxxiO=w1274-h708-no)

```javaScript
//ES5
var Person5 = function(name, yearOfBirth, job) {
	this.name = name;
	this.yearOfBirth = yearOfBirth;
	this.job = job;
}

Person5.prototype.calculateAge =
function() {
	var age = new Date().getFullYear() - this.yearOfBirth;
	console.log(age);
}

var Athlete5 = function(name, yearOfBirth, job, olymicGames, medals) {
	Person5.call(this, name, yearOfBirth, job);
	this.olymicGames = olymicGames;
	this.medals = medals;
}

Athlete5.prototype.wonMedal = function () {
	this.medals++;
	console.log(this.medals);
}

Athlete5.prototype = Object.create(Person5.prototype);

var johnAthlete5 = new Athlete5('John', 1990, 'swimmer', 3, 10);

johnAthlete5.calculateAge();
johnAthlete5.wonMedal();


//ES6
class Person6 {
	constructor (name, yearOfBirth, job) {
		this.name = name;
		this.yearOfBirth = yearOfBirth;
		this.job = job;
	}

	calculateAge() {
		var age = new Date().getFullYear() - this.yearOfBirth;
		console.log(age);
	}
}

class Athlete6 extends Perso6 {
	constructor(name, yearOfBirth, job, olympicGames, medals) {
		super(name, yearOfBirth, job);
		this.olympicGames = olympicGames;
		this.medals = medals;
	}

	wonMedal() {
		this.medals++;
		console.log(this.medals);
	}
}

const johnAthlete6 = new Athlete6('John', 1990, 'swimmer', 3, 10);

johnAthlete6.wonMedal();
johnAthlete6.calculateAge();

```

## 15. How to use ES2015 / ES6 Today?

[Babel](https://babeljs.io): Use next generation JavaScript, today.

### 15.1. Environment Setup
- Intall NodeJS
- Install Babel
	- npm -v
	- npm install --save-dev babel-cli babel-preset-es2015 babel-polyfill

### 15.2. Usage
	- ./node_modules/.bin/babel --presets es2015 script.js --out-file script-transpiled.js
