---
title: 'Advanced JavaScript: Objects and Functions'
date: 2017-04-06 17:29:12
tags:
- 学习笔记
- tech
- JavaScript
---

## 1. Everything is and Object: Inheritance and the Prototype Chain
![Everything is and Object](https://lh3.googleusercontent.com/I0PB8RP7AO9LkCeT8eT6nVUMBSYDY2PyEfxlf_eum2bGhpxX_uy-S79Ork__5s57wNLgiz_s3WnltNj-te3j2av-KpJ2BjANLJh2IpST8waederhveRbfDqnAwQQgIPCQe6t3YFVXnG2nigrXIRz5Ph1QzSggrPrN-3HTP-NPfzHL6LbRWKhs0KwDDvF_FyXmn7o4Z-AwtK2PCf-8VdW_BktnK652XbVRnvRYKVnvYNhPmLH9Mu_X114V5Uw6HhflHTFy6WY3g4kQ7BzSfnM-jrSWVic9F8XHlUX_GXm5C6lpg3O7ATI31xuyIQuI6ElPIQ1fhJw3b9ZhJrtZworY8rSU7ESkSJoGt2O5C5LEaCcbiboKFcHlRlo7m1Tv63St7buD4IxPtQF1UZjXlU4mBnAw4nSBEXkt_r7v8jYCJZ_I3IyzNEZZcVWFpaNX5VWAbTKO77mXRikSSCR1FNBDdoPDQTFhnQXeqkJLZsHXLYXCi4c_QVSdeeoXJW990CoWB1rYFN3ZfQShvKxvL7sAJ8a_-HgRUguBXTBHHnrA2S4yWxiEv6oHC3u_mwLzuqKkLc_0rH_t4TAtdyAep3MpjIzeOh9-c72LGGjfEub1aiX9no-TbpB5OD82uPKhtKSywuOqZbCwvEwugp8fzKtI_Miah3Em9klXzMAPk6c2g=w759-h282-no)

### 1.1. Object-Oriented Programming
- Objects interacting with one another through methods and properties;
- Used to store data, structure applications into modules and keeping code clean.
![Constructors and Instances in JavaScript](https://lh3.googleusercontent.com/JWGejWy-5UEIY4S3q6FNXkq3b7H0PbECFGRFiOlE3rDsvqY2c3yaTPwXxlhes7NNcz77vfBSs2nFME6GNEP9kDajiGD62-bjE3YxFQX2Jyr4Cs40IDTE4fNWFc9JHUfXgi_SbsHvCPEncJA1Fk_MH5rqCtMEEp-YIWFT2X5EBXAup910lnt_HqTB7MAR-Ipgx_gIN-WejB8q1p3x3goAK-fhykFYNnRvcLO0hJhQDb6niwYET13BlHgvehiFaESb9R9LJ4Uq_9iyaBrqisZBmWN45PIOggWbcqWiZf1tFo6_Ah-o00SAEey_MwdwpntmzZi7kBZA4gq2ibHmakHCq2t_i8760yenwMPPhrk7unDNiMHnqp3fYxjzOvNTc-NKxOl-1oJFbiwdyNU_TwccbfsGhCwtJg8tQmVbtTSdy_Vv-FUayhc0CPQiDHirDNwCkqRX5oWHkfcMfynVNyERU-weB-5J7ReTRUgWsfKe60BfQx1emhwjJ0wI_0rmlN4RN_2MjDEz3cwSUgVUmZw1z1JzYoHy8A0Uz_VWIi0Y59ysAnYXVekqwqp7jNtmsfMrtoemq1caDe7J4EQ3u8iVa5YbUk8d4ijud9e-AU1urV0EbFIn-xYrtIYZFWRf_yuK5Sqap7e89CiBd6tq9sHLteR3201C_Pcy0vsQmWwfZA=w759-h341-no)

### 1.2. Inheritance in General
![Inheritance in General](https://lh3.googleusercontent.com/pnHefeMqK3jMpAa0wTuxhgPzLPVHnuKXMPIRjRmDcjYJKU--kUg3sTx_uLi3qUsy9RVv3eTTOOdMiB820BPtAn6T8rG4XXQVgLnPVYVjyX_IgqS-RDt6gCH_HcLDP4SzkEfC8HUoJ2J0Ta6IxPNchYbVeYMInXzYQQv2bnnzURj4RCkAwKetJt7p04TAE-DEDHAincw5Uka5Lnay15UerYnTw4rglVn5s3anVJM5Hwy2PJ3VOY1M9RvxIJl1jgo1EvtoAkAAYaGHABIyoFARF6KfDWHFqxgM7N3WEzUDkaihSNBbHMloH3mDQHGyq5y7BJHBa9HUzwJgAbvrcPd53p22zPrFdTYn1YgQjFyc1mcf7Fv3I_cRptrG7JKHIxnvneF9-tkAXnAmvYiWd5tUJLN7ULre_GPj_G4kNh7qnk1hxocBXhao9p58bnJG7dPJdbyUZ98RXawaMoKZFDFlMxPu2r547fAgTUI8q1kV2JPw5dALyjU_HxE9auka0zvWebpQ3PCIEZJYLsVwVgPNW82-8t-LpIlIyuqv0xK7JfVoGanAc3T6ep3OuXg3P33S7U7MnOF9Qa9BF-ldGAhVNo9nxZBAfitFzTqwNcOJM7pgLbiOYhXDSkAEbPhwp3wrSk7FCpLnyjYjCXRjJS129YvZ4RcSaH75pE9wF-idPQ=w759-h351-no)

### 1.3. Inheritance in JavaScript: Prototypes and Prototype Chains
The inheritance in javaScript depends on "Prototype" property.
![Inheritance in JavaScript: Prototypes and Prototype Chains](https://lh3.googleusercontent.com/Ie7W5tqMOWICPnqSRIBksRmmfr8NGJbZ4r93oUGN_u-JxnJcFhQB60bDZDxV0gd9HdQpjSwq8XIcj8rXJrR6ivzc-Z1jsI-wljf873uGJONSe47-PkV1oB0C33ZF11yKkpIzyBhPFz4ZSWIED1w-VloXoafyxR5Xv0VL7TgmgRo9psFF1sI9oknV1qbPWNgrrvDjVJSholHkuCp5Cdnvj2t7xCLaChPFKe6wg7PsIJ58-RS_kHTBpR98XQvsPWhWTB7MVD9K8o5cw508Hcjvfgbl6RIpHCfYNOAz9DpWYyV0ekJX6oAt6hlL34OLoizipotSe2eWwz8B3EEd7YIYzmjEJW9ZfOMEkCPVTjYOnuF-RUvShhqwvV-yAcAwF2Y5LTyzoQnTt6VbxNT5lB5kH_gX3czTcxDa-BblwR_nL55_y8KiMU7SlV58VN3CFY4VC5oU9eeL9HlEmWDR7sZmPHEHxbEzTYiQqseE0_out0AbwO5KmfEN4X1Zw6NHvSoDyh1f3sa7mpyZBzBIxK5pvcQFQtvcRGySzrJYDZYmdGaIl53LfUhgpojZDLZNFFREJupIPtXVkqKkBI-LhlbmW6wW_xDlFcca9SNVWyrFSmd4Fw5qoQBFC-NuaF1HIeYZ8Sn0rYJ4n-16w-ShYkyPU3u59A7VmtTO_MevLdaZQQ=w759-h364-no)

### 1.4. Summary
- Every JavaScript object has a **prototype property**, which makes inheritance possible in JavaScript
- The prototype property of an object is where we put methods and properties that we want **other objects to inherit.**
- The Constructor's prototype property is **NOT** the prototype of the Constructor itself, it's the prototype of **ALL** instances that are created through it.
- When a certain method (or property) is called, the search starts in the object itself, and if it cannot be found, the search moves on to the object's prototype. This continues until the method is found: **prototype chain.**

## 2. Creating Objects: Function Constructors

The first way is to define all properties and functions in constructor:

```javaScript
//Approach 1: only use constructor
var Person = function(name, yearOfBirth, job) {
	this.name = name;
	this.yearOfBirth = yearOfBirth;
	this.job = job;
	this.calculateAge = function() {
		console.log(2016 - this.yearOfBirth);
	}
}

var john = new Person('John', 1990, 'teacher');
john.calculateAge();

```

The alternative way is to use prototype property:

```javaScript
//Approach 2: use prototype property
var Person = function(name, yearOfBirth, job) {
	this.name = name;
	this.yearOfBirth = yearOfBirth;
	this.job = job;
	this.calculateAge = function() {
		console.log(2016 - this.yearOfBirth);
	}
}

Person.prototype.calculateAge =
function() {
	console.log(2016 - this.yearOfBirth);
};

Person.prototype.lastName = 'Smith';

var john = new Person('John', 1990, 'teacher');
var jane = new Person('Jane', 1969, 'designer');
var mark = new Person('Mark', 1948, 'retired');

john.calculateAge();
jane.calculateAge();
mark.calculateAge();

console.log(john.lastName);
console.log(jane.lastName);
console.log(mark.lastName);

```

## 3. The Prototype Chain in the Console
In console, if we type in 'john', we can see the john object gets printed.

![Person Object](https://lh3.googleusercontent.com/Q_0HsZL7t4aZMpmPfVEvvRWFZUqCQ8tZh7rAOLxM0oQ4Eg7urj4NxhKuwUq-b_8rwOVi21l__rgCx9pX8fW-YEkBFL1iT-sX_HMo_GQ6qibDHAwqF8tTl-FRz7pMtVllEzGN_-aKDGEYPVhzT7rrZhtzfV8biOAbiwIwP1AsPPCdTtxDxPsjqfj4lyb8_HW5vsAbOwJayWgSLYVkSAwi6PWoYQm3-OuLARqto7l4XHy6BqEFB4k8tgtXhtF4ldN1_YCYpuugETcSLh0cRoPDaAeFdgMw_GU-prQtU9k3g9BdHOmoG_Kvz9n_PcTu5B9YzKuut_B1Un0iCMGyqAQWRdLBsJaPJGPCsOmUAp5JUOCkmOpzS6IF4QxxPjZXAE4yA-bZMdw5-PQRALSiWJirQ5a1tZOgInWQCEgP6oO8mSpTss2V86-x315Aw4oT8LcVOxFTWp09bdHJi6REtWyOJUzanOBMbnhANlCRg0xRHkEuLhlNpFP3KdZ9wry9KcpoXQdgpU198CvQk3KyeFWC64t4ZtQZEFIracg310oNlL4swfmO7BtbF5JfIu9oVC401iCx9cO6YFAP2Ab0T9pdlLmsfwwjxB09PeiKaYNyYzrmqA2ghD1xPm3AQn2HJxQYS9fomjXondjoYWrXMXrpgKbyAUcl6US8UkpNEsmY7Q=w759-h415-no)

From the above screenshot, we can see Person's prototype is an Object, and also
```
john._proto_ === Person.prototype //Return true
```


![Screenshot 2](https://lh3.googleusercontent.com/zVLqL7_JKgTh6VB-9-CrTa-dPWKk7RoI6ZX_k9FhwBpmF54dxI7TSXZ43k1veNWNkrcKjVfpcc1SV2UaQNYfQLQN1NxXM2Re41jBCbLvJsQ6v3QUtwJeEfUpydUzqle6Xr63zjuJtX7jgEXb4QwXviqB29y3eNbqmfGxpg-vwsvaKqADnYvlTATYoVv1XwB54dnyAFCsFTQyiEkMmaj1ejpu7raJbv-DMD4sfBKc2lY4562pU8EZo0J5u6XLNoYlVwvemDRQ2FmUl2ISeQeQaIE4QstfxuRaJdToX0KMvJ_Ce_2R6EC6p1FQJhVQ7KlD0s827XN2zE2SNwAlroYcriXYGiH63_JH2_rXSqgr8FTr55TzlwtYw-U2BT1jfP2pdfYqkJm_a0tRDsLniw12TEew0-eFm2LZc1jn92T11EvcEMafz0zXUn6b3rItk9lCHqMjGATr5FeYM8N6D9-US1sXgWV9Q9T0tzfe619JuvsLthVKX6Uva7CVzWc86aDX8RJFsdNBq6Jsy-26-mmf4VskLtFEh3DO7IqMx2m1r0dnBB7KvsSGPa7pF4XSu0zWsUHIWI1sVyL9FHVDeb71rZUG0oLwITS2jcRlHbAQweyAqRnLLZz1o69UaYvonxvAg8ISxWUpNe20WOtrY27KceFfi3Qn5ChCfEOesssHaA=w759-h588-no)

From the second screenshot, we can see that because of the inheritance, the john object can call hasOwnProperty method. Obviously, ***job*** is john's own property, but ***lastName*** is not.

Another method to know is ***instanceof***, we can know john is an instance of Person object.

Here's an additional example:

![Array Object](https://lh3.googleusercontent.com/O0cEhZETj1K0l07nXPUJYM25MTcjuIqswjbxV52MPBNACSo8_Tbk92u6wz8Sdmcdf12rHeDOQ8VB3AWEtPEM2V_2nvRgaOkAU7Vnvtt2eCWCbZO9plRt8bRVI93L881u65p6Ua0DiADigwr1xvqnzOcE4xHsB34N23_AWYAwZ7GT4wkDWZL7USuBxYChE0B2bGbazuFMRuIvUQmEA0d1jD__xAiIrvcNiiP84YJ3l1Gny8WkffV3584AG5v0hria_7CwZrbdGCVqqPj0lcVEGxNOtF0A3eT37SRu6Z-nZ2yRRW7aJs564XgGjP0vm50w3htyytBo7KSAE2BNx97IIP0uJNxcZVZFsXWfqL7NS0W4EI_znZp7WRy2SWxs7CgF3om4orBxBzHEu4NZ9xXD8FGjXiPNYp-X4IbBaf1INIm3_54xyscIwnT4Abhun7jq3ad0mZ3adGorimhoLB2QOHzrSLCvDck0z6eMGW24mKOUomvoLkwK7VEsHXprNs1HiQ9n9ZZADk6ZEB3Rh_oMBuU6CAi-wagCA8ka9eo3Bf8t-w_aDP2tK2WCNgjHED4vsSMdnO50qU7BGzMjGjChwtyy4zKGI_Z8twLVttrsw15HvTYDDvnN-NseKKCig_wA9T9wRBOyDZ-AMTLaN6w37beltoHUEaMwfJPo9_2EaA=w759-h350-no)

By typing console.info(x), we can see this array object. If you click on the ***_proto_***, you can see all methods available in array.

![Array Object 2](https://lh3.googleusercontent.com/5NIUrcZs-QACaZ8ebMunMcCrWK_8HyObYoiXbUwt6T4S0PBdGgnQ6QhFDN9jcaOqvgzAsQcD9pCo-sFs5jqQBwciQkZN8eBCUqrD2Xu06UEbOAwRxQB-HYiKVWGdKwwLHtefUI0l58XXgh60lHN9DXd70q4agaXxHGdRN_usf27G3_c9_ein8ODosaQxa6lat5ZAEK3UVqJV_g1TIGTBqhATly0pHmlsI3qSxOKZTub8J0tpBWCf5AdQEIpWZDVmwlOrJlp4Af8GRkgx6pG7iRmDeY8AzSp2wbPsoIkpItZCY8wdRFDv3jvb_bIcuYPIph4bBd21RsBeMvCI6C8l8NJcTVicZnBnpsVzYkmb1lGprG_L5TIdgY2v_2hn8QBLgkatqnCY-nuEiE1fnPMUWFNjfFqgPsSnYJ9joQrGmVge1be9RiGoyuQ75wk0036gTS1E0Td5lP28NBYzHzYOMOvNwSLotM7SV4_4Xamx7I9z2dX7aoWpkNZ5S-NVJrS4rekeRU7KFErXtoAcXFuGnx3bpaPTdXtNCVDy9XCrKTblmwrQuGxCW3bk3iotfpJeQazYhS9MJxtxnkpHHL9Fcsy0JgnnsvA3Fu55wF4qRUfR09bK-EOdiq_oBPhnYCfw1MOCblNzQcrs6P5Jdbmo4587MydApziXt8zuFvJzXA=w759-h381-no)

## 4. Creating Objects: Object.create
```javaScript
// Alternative way to create object: Object.create
var personProto = {
	calculateAge: function() {
		console.log(2016 - this.yearOfBirth);
	}
}

var john = Object.create(personProto);
john.name = 'John';
john.yearOfBirth = 1990;
john.job = 'teacher';

var jane = Object.create(personProto,
{
	name: { value: 'Jane'},
	yearOfBirth: { value: 1969 },
	job: { value: 'designer'}
});
```


Object.create builds an object that inherits directly from the one that we passed into the firs argument.

While, on the other hand, the function constructor, the newly created object inherits from constructor's prototype property.

Actually, one of the biggest benefits of object.create is that it allows us to implement a really complex inheritance structures in an easier way, because it allows us to directly specify which object should be a prototype.

Read more: [Understanding the difference between Object.create() and new SomeFunction()](http://stackoverflow.com/questions/4166616/understanding-the-difference-between-object-create-and-new-somefunction)

## 5. Primitives vs Objects

Variables containing primitives actually hold that data inside of the variable itself.

However, variables associated with objects do not actually contain the object, but instead, they contain a reference to the place in memory where the object is stored.

So again, a variable declared as an object does not have a real copy of the object, it just points to that object.

See the example

```javaScript
var a = 23;
var b = a;
a = 46;
console.log(a);
console.log(b);

var obj1 = {
	name: 'John',
	age: 26
};

var obj2 = obj1;
obj1.age = 30;

console.log(obj1.age);
console.log(obj2.age);
```

In console, we can see the print out as follows

```
46
23
30
30
```

It shows that actually obj1 and obj2 are pointing to the same object, once obj1.age gets changed, it reflects to obj2.age as well.


Another example

```javaScript
var age = 27;
var obj = {
	name: 'Jonas',
	city: 'Lisbon'
}

function change (a, b) {
	a = 30;
	b.city = 'San Francisco';
}

change(age, obj);

console.log(age);
console.log(obj.city);
```

When we pass a primitive into a function, a simple copy is created. You can change a as much as you want, but it will never affect the variable on the outside.

For the object, instead of passing the object to the function, we just pass in a reference.

## 6. First Class Functions: Passing Functions as Arguments
### 6.1. Functions are Also Objects in JavaScript
- A function is an instance of the Object type;
- A function behaves like any other object;
- We can store functions in a variable;
- We can pass a function as an argument to another function;
- We can return a function from a function

Because of all above, we say that in JavaScript, we have `First-Class Functions`.

### 6.2. Code Example
```javaScript
var years = [1990, 1965, 1937, 2005, 1998];

function arrayCalc(arr, fn) {
	var arrRes = [];
	for (var i = 0; i < arr.length; i++) {
		arrRes.push(fn(arr[i]));
	}
	return arrRes;
}

function caculateAge(el) {
	return 2016 - el;
}

function isFullAge(el) {
	return el >= 18;
}

function maxHeartRate(el) {
	if (el >= 18 && el <= 81) {
		return Math.round(206.9 - (0.67 * el));
	} else {
		return -1;
	}
}

var ages = arrayCalc(years, calculateAge);
var fullAges = arrayCalc(years, isFullAge);
var rates = arrayCalc(ages, maxHeartRate);

console.log(ages);
console.log(fullAges);
console.log(rates);

```

## 7. First Class Functions: Functions Returning Functions
Functions can also be returned from functions.

```javaScript
function interviewQuestion(job) {
	if (job ==== 'designer') {
		return function(name) {
			console.log(name + ', can you please explain what UX design is?');
		}
	} else if (job === 'teacher') {
		return function(name) {
			console.log('What subject do you teach, ' + name + '?');
		}
	} else {
		return function(name) {
			console.log('Hello ' + name + ', what do you do?');
		}
	}
}

var teacherQuestion = interviewQuestion('teacher');
var designerQuestion = interviewQuestion('designer');

teacherQuestion('John');
designerQuestion('John');

//An alternative way to call
interviewQuestion('teacher')('Mark');

```

## 8. Immediately Invoked Function Expressions (IIFE)
Here we use a silly game to demonstrate how IIFE works,

```javaScript
(function () {
	var score = Math.random() * 10;
	console.log(score >= 5);
})();

(function (goodLuck) {
	var score = Math.random() * 10;
	console.log(score >= 5 - goodLuck)
})(5);
```

IIFE can only be called once and has the advantage of data privacy, because unlike defining a function and assigning it to a variable, IIFE can not be reused elsewhere.

## 9. Closures
### 9.1. Code Example
```javaScript
function retirement(retirementAge) {
	var a = ' years left until retirement.';
	return function(yearOfBirth) {
		var age = 2016 - yearOfBirth;
		console.log((retirementAge - age) + a);
	}
}

var retirementUS = retirement(66);
var retirementGermany = retirement(65);
var retirementIceland = retirement(67);

retirementUS(1990);
retirementGermany(1990);
retirementIceland(1990);

```
### 9.2. Closures Summary
`An inner function has always access to the variables and parameters of its outer function, even after the outer function has returned. `

### 9.3. How Closures Work
![Closures Summary](https://lh3.googleusercontent.com/_lr3ZJ3wVRwrgDWcyInIPTNFGApLSYBWiSFcDPj73XFMmyr0RlEaSMUFr7INnkRwhVRHlX_VhiFci4DcUXRWWAiiLXh5zpBG93DxaXLmaCNGYorfBwqQ_nJYsuBPNzMmzMItQAeGWfQQp6GUbWiodzP8oYT7hHfC2NgqSFe7cioAEnh3WKBFIQ4ttY1B49-Dpj4TshizgMTMmabOmqi77ZDGVjDZyHkGD4_cc_6VFULKBPqOFjPGrwjlXPvK-MTrgsedUcgsB3CrW6L_6o7xdn9s9zcGtHu91cUl_QnTJ21gzau-qdKHN0-7nO18IAx-4nlNRAxuU9ehvXft4NrMLow7rOm5_VxUCpq8vPQ85MYO6QSoBygqgzptHYYF7YWRdCQGcWorpfQqroTqTq8Z3BPln354z260f0tko2N7ymdG_Oc0NUwrAMVKiymT6zoGoL-Fc05oABRAjSknQTBhSM_g9lIdgtIE2AAafIV_NFDx3LMTF_R4vMLrL23X3DxWpNGgW3cbHsYobXxOPVgon8TtbjNtQaAC2QxiNiHmksFk-Ce-JtzUV4coXHXZhve1__yJmCmu4Z5pWPjJXC1f2rUmPDWDwKNgPapP2JVjg3GHKnaiQJgNxnzg9-VzchSs9us1cuDg9WZMCH8A3_MXB9AZ4drDQaMUMlz3wcnlzg=w759-h334-no)

After the retirement function returns, the execution context of retirement function is gone from the Execution Stack. However, in the scope chain, the retirement function is still there and keeps working. Therefore, we can access the variables that we were created in the retirement function long after the function has completed execution, and after its execution context is gone.


### 9.4. Rewrite Interview Question Problem

```javaScript
function interviewQuestion(job) {
	return function(name) {
		if (job ==== 'designer') {
			console.log(name + ', can you please explain what UX design is?');
		} else if (job === 'teacher') {
			console.log('What subject do you teach, ' + name + '?');
		} else {
			console.log('Hello ' + name + ', what do you do?');
		}
	}
}

interviewQuestion('teacher')('John');

```

## 10. Bind, Call and Apply
### 10.1. Examples on Bind, Call and Apply
```javaScript
var john = {
	name: 'John',
	age: 26,
	job: 'teacher',
	presentation: function(style, timeOfDay) {
		if (style === 'formal') {
			console.log('Good ' + timeOfDay + ', Ladies and gentlemen! I\'m ' + this.name + ', I\'m a ' + this.job + ' and I\'m ' + this.age + ' years old.');
		} else if (style === 'friendly') {
			console.log('Hey! What\'s up? I\'m ' + this.name + ', I\'m a ' + this.job + ' and I\'m ' + this.age + ' years old. Have a nice ' + timeOfDay + '.');
		}
	}
}

var emily = {
	name: 'Emily',
	age: 35,
	job: 'designer'
}

john.presentation('formal', 'morning');

john.presentation.call(emily, 'friendly', 'afternoon'); // Call

john.presentation.apply(emily, ['friendly', 'afternoon']); //Apply

var johnFriendly = john.presentation.bind(john, 'friendly'); //Bind

johnFriendly('morning');
johnFriendly('night');

var emilyFormal = john.presentation.bind(emily, 'formal'); //Bind
emilyFormal('afternoon');

```

### 10.2. Rewrite the Age Calculation Problem

```javaScript
var years = [1990, 1965, 1937, 2005, 1998];

function arrayCalc(arr, fn) {
	var arrRes = [];
	for (var i = 0; i < arr.length; i++) {
		arrRes.push(fn(arr[i]));
	}
	return arrRes;
}

function caculateAge(el) {
	return 2016 - el;
}

function isFullAge(limit, el) {
	return el >= limit;
}

var ages = arrayCalc(years, calculateAge);
var fullJapan = arrayCalc(ages, isFullAge.bind(this, 20));

console.log(ages);
console.log(fullJapan);

```


## 11. Code Challenge： Build a Fun Quiz Game in the Console
### 11.1. Basic Level
1. Build a function constructor called Question to describe a question. A question should include:
a) question itself
b) the answers from which the player can choose the correct one (choose an adequate data structure here, array, object, etc.)
c) correct answer (I would use a number for this)

2. Create a couple of questions using the constructor

3. Store them all inside an array

4. Select one random question and log it on the console, together with the possible answers (each question should have a number) (Hint: write a method for the Question objects for this task).

5. Use the 'prompt' function to ask the user for the correct answer. The user should input the number of the correct answer such as you displayed it on Task 4.

6. Check if the answer is correct and print to the console whether the answer is correct ot nor (Hint: write another method for this).

7. Suppose this code would be a plugin for other programmers to use in their code. So make sure that all your code is private and doesn't interfere with the other programmers code (Hint: we learned a special technique to do exactly that).


```javaScript
(function() {
    function Question(question, answers, correct) {
		    this.question = question;
        this.answers = answers;
        this.correct = correct;
    }

    Question.prototype.displayQuestion = function() {
        console.log(this.question);

        for (var i = 0; i < this.answers.length; i++) {
            console.log(i + ': ' + this.answers[i]);
        }
    }

    Question.prototype.checkAnswer = function(ans) {
        if (ans === this.correct) {
            console.log('Correct answer!');

        } else {
            console.log('Wrong answer. Try again :)')
        }
    }

    var q1 = new Question('Is JavaScript the coolest programming language in the world?',
                          ['Yes', 'No'],
                          0);

    var q2 = new Question('What is the name of this course\'s teacher?',
                          ['John', 'Micheal', 'Jonas'],
                          2);

    var q3 = new Question('What does best describe coding?',
                          ['Boring', 'Hard', 'Fun', 'Tediuos'],
                          2);

    var questions = [q1, q2, q3];

    var n = Math.floor(Math.random() * questions.length);

    questions[n].displayQuestion();

    var answer = parseInt(prompt('Please select the correct answer.'));

    questions[n].checkAnswer(answer);
})();
```

### 11.2. Expert Level

8. After you display the result, display the next random question, so that the game never ends (Hint: write a function for this and call it right after displaying the result)

9. Be careful: after Task 8, the game literally never ends. So include the option to quit the game if the user writes 'exit' instead of the answer. In this case, DON'T call the function from task 8.

10. Track the user's score to make the game more fun! So each time an answer is correct, add 1 point to the score (Hint: I'm going to use the power of closures for this, but you don't have to, just do this with the tools you feel more comfortable at this point).

11. Display the score in the console. Use yet another method for this.

```javaScript
(function() {
    function Question(question, answers, correct) {
        this.question = question;
        this.answers = answers;
        this.correct = correct;
    }

    Question.prototype.displayQuestion = function() {
        console.log(this.question);

        for (var i = 0; i < this.answers.length; i++) {
            console.log(i + ': ' + this.answers[i]);
        }
    }

    Question.prototype.checkAnswer = function(ans, callback) {
        var sc;

        if (ans === this.correct) {
            console.log('Correct answer!');
            sc = callback(true);
        } else {
            console.log('Wrong answer. Try again :)');
            sc = callback(false);
        }

        this.displayScore(sc);
    }

    Question.prototype.displayScore = function(score) {
        console.log('Your current score is: ' + score);
        console.log('------------------------------');
    }


    var q1 = new Question('Is JavaScript the coolest programming language in the world?',
                          ['Yes', 'No'],
                          0);

    var q2 = new Question('What is the name of this course\'s teacher?',
                          ['John', 'Micheal', 'Jonas'],
                          2);

    var q3 = new Question('What does best describe coding?',
                          ['Boring', 'Hard', 'Fun', 'Tediuos'],
                          2);

    var questions = [q1, q2, q3];

    function score() {
        var sc = 0;
        return function(correct) {
            if (correct) {
                sc++;
            }
            return sc;
        }
    }
    var keepScore = score();


    function nextQuestion() {

        var n = Math.floor(Math.random() * questions.length);
        questions[n].displayQuestion();

        var answer = prompt('Please select the correct answer.');

        if(answer !== 'exit') {
            questions[n].checkAnswer(parseInt(answer), keepScore);

            nextQuestion();
        }
    }

    nextQuestion();

})();
```
