---
title: How JavaScript Works Behind the Scenes?
date: 2017-04-03 08:11:19
tags:
- 学习笔记
- tech
- JavaScript
---

## 1. What Happens to Our Code?
![What Happens to Our Code](https://lh3.googleusercontent.com/O55ygo71OcIq1ZWkeq5MmJgJvngfikY68Y2u-P3HGg4JhMIQ_Nl4WA1LwQnpnartTQjnIrbanKGdCkUy8AUdY3nzu0qhpi_P7wZ0LOn_B8GF5Ot5PvxlP6IfR-OO4eCQhUHC6-MwQH1HL7gzV2JpmNSjT-D_8yrts5VVjXuuLItm5Rfm0bslWS2jZqIGJeuXg1Nd-eojrgVbMS3nL9P0R6uEbwpKXPrGu77WoTalhjbgKM-QLzdpsB0c7y9JqLHHobxqjrHI9Wogz0Szkcu0RfnB-1HryWlzsrollu8ncuzm8t730UV8GVNnviVSjWwlgEkeGPIDF1bonP1iFNLTVK7FdWtW11xxM2cuhjhdMp-jQnZjNpHoisOxEX0Kv7v81TOPQFukptupXiC42FuklYnqrUc1wLLhekUXwJSyKAxS93lvxSvxIWSuKJR9JjbgY3ZXwnst7K6A4YXwvqXoO2U71R6btXJK0YFiNN4coUO_VdDRqqq-EddpJrOzgUpf46BUlRhZ4S0HUbgfzFUbdhpllQrFC0kWQOwuYhVRHp7MASml8l6QsQsbPE1IFJ4u20yDwmuvA9g75i339JNGPKtmpo40tTA_Way8X434_oCKlUwx2JuAeBMLIF-2RIsOA-DPPniHT2HBp6uYQr9CvfsX1xVHQwOSqQKEP9cRFQ=w1440-h558-no)

## 2. Execution Contexts and the Execution Stack
### 2.1. Execution Context
![Execution Context](https://lh3.googleusercontent.com/i7-xaGbNE0MKmlhdicghBytDi0k7AkekQBcPbc9HcXf2Lwn8cEx0Nr2UBQGlUVW1MUgzLsRt9o5KVeD7MIXPSIfEy33wWJSesaRJsJsgH6QBBKBNcl39YM75gMaT9XrQYbBDmyb4snP0d4Loz0Tpngo-BMLZ9jsVfzMTbXFww5f8PYHwFTJ7O5nB00sss588aILyLHQyps7mGpl_ZMSHL6Xkw3sWC-4Q1efkT-BGoSfkS8-swaE-Pm1AiH_5_OFThjcpobfh2pyOvDbs7Xb9sYmURhNuBBVsFSz5YUQtrb4jcL5tO6aUtQu6OYAhHVpk7Vf89JN2Iqxp7dGPIP9QPD-DOM-_mLAhvmUDWDeTMFyCQbTRweycYC-9EFlpaOcKLCuuTWQnqgynyaOFT59rO040W_-OvqnH1rIQli4TZxRGxJmTeU6EsTzUVq0t3p67AFMpEGJu-LHRB3_f7KcU-aqZOenwdIgj-6eNvWtTZzaDVOBD2O8MG8mB_Jdfh5cpruhWKDPdgYChfPyvba2PtVhgj4KRk8K-lWttQLrZexVC0OJR-sxtfZ8bCDNp4Z7TQbHI0zmKBS02sEa91ecrRr_2PnXLF3RgxR8AmxMNs-_cs2ZhFcM_tWqwkJlSdrIVLm7f1_2ZuKKnGhaCtgSOHDB1_7Sqa0SuD6n2Y_yiOw=w698-h838-no)
- Code that is not inside any function
- Associated with the global object
- In the browser, that’s the window object

```javaScript
lastName === window.lastName
```

### 2.2. Execution Stack
When executing the code inside a function, a new Execution Context will be created on top of the existing one.

![Execution Stack](https://lh3.googleusercontent.com/Kslrk3U4J-QrkOX7zp3hUC2UIBxorVssUHX_ybRAUKELW8686sptO1exa9rM-87sI5A30N74aIQZh8NyCeqVQO1D469aNIbH8TwFFs1ybPcx1a0Xpg9_m84GrM3S6lkSgr3zWsN5KZrG3P34mWa_Zz_fWzz_7MFmjqsChDcrNLqazE8wkwGlbLt_bb_aaleUh26GEwCD_Wvgv5ijvPK2QwJnU6I2Wm-JMXZENdSxhPuijJD-6ve7T8MqlJ5H6Ufi1WuzXKSs-llulsMfBPkAz2LitwjGhKoPibij8ObYlgILT90EK6ZlR8qKbnCG193CJfG0EaO98UQaZ6ZHJBSDRW1C5gQEcAtYCSi5bM2RCcVFZAZV8zBEVwec4yfd0iQHlNGklpphLzwv7zPG3yhtwav9VWq-ORP0brJ2i7o3ISIKFT5IY8sO8NWNkzx9EN7jg2TEU58SSKNXatjG52l0bC-_rWuK4bXpennNZl142UzBkFGsRn6Rw89ePPQcyhlSA98gw3veq4DLjIufio3Oo6_jxdxP-MHP62W0_B5L81e8EqoNrbt_MO9XwZLJtKaamt_56_L3qe3L71mCmYVqAk0CoFLrn8qXF-_LQmRjWGNwGfOtgMlLeEKweqov4KTou7oPyZmIQ0WDyTDmK3O4rTLy3uAJXjhNMRBNqXAg0g=w1440-h805-no)

## 3. The Execution Context in Detail: Creation and Execution Phase and Hoisting
### 3.1. The Execution Context in Detail
![The Execution Context in Detail](https://lh3.googleusercontent.com/pf0WfjuVDh6ufRtT5lKLPEF0G5yAbSS_toYzm_HZh-dNcvEz8dadve0vF2j8P8ZUa7k0SIEjGHc4_qZXLPg8Yvs5Gb8QTKtKZRXgBmSdXNwASi4XUm4UmiDg4E6pVE0o2W_WoXhjeXp9tZByuTkGpTXV0Io_zR9f1gXkaszM2sAzjRkxOXN5AwoDR9NmUhkIaYa6_BF0_H7dpBlqOJO7GErgmE0-71a-mctQBR2dnRyO4nMcCB5KkYp-rNyZd-NESd8I_XMPWA1CtRpuJ9z0MNq4iXrlXt7FgmPD-iJ32Mx9xaLiwC778u_C1Os-sdVy_F65iUrtEqNXTekoQh16aVDcRF2bdPUX7Ph7WV3Bvl4M6TYg17PokRxg-YvVdT3SR4s0IcfjKCMwb49OIS3iHPFRv78qS_E8X1yv8XwXazEnqRSRSmCBk3Z_iFqPtEV5OOYo7wlMNnVBemhsZ7dMqPrpnMbJhRE5YvVp3k32gCEA5GTVtVoYXAUxcerwVQZRlonhnT6OXeDVrPXTRtqVS0nh84hx0TeLTsBzXdjkAKG0f4mBMC2_AWX0e9NeLWtTFLAIsXJl15xYGK9aiVm1d_VA2Z6D1mSB-BhPj5qpYS6zFQwWhhCD-JqbjJZG6ETL8_bpdmebNCFVNzcxk7WsR5LK8ySID_IecQJPn19TfQ=w453-h544-no)
1. Creation phase
	- Creation of the Variable Object(VO)
	- Creation of the scope chain
	- Determine value of the ‘this’ variable
2. Execution phase
	- The code of the function that generated the current execution context is ran line by line

### 3.2. The Variable Object
- The argument object is created, containing all the arguments that were passed into the function.
- Code is scanned for **function declarations**: for each function, a property is created in the Variable Object, `pointing to the function`. [Hoisting]
- Code is scanned for **variable declarations**: for each variable, a property is created in the Variable Object, and set to `undefined`. [Hoisting]

## 4. Hoisting in Practice
### 4.1. Function Hoisting
```javaScript
caculatedAge(1990);
function calculatedAge(year) { //Function has already been available before executing
	console.log(2016 - year);
}
```

The above code works because the function has already been available before executing.

However, for the following code, it’s not working, since retirement has been created, but just set to ``undefined`` before execution.

```javaScript
retirement(1990);
var retirement = function(year) {
	console.log(65 - (2016 - year));
}
```

### 4.2. Variable Hoisting
```javaScript
console.log(age);
var age = 23;
```

The above code only prints undefined, which is as expected.

```javaScript
console.log(age);
var age = 23;

function foo() {
	var age = 65;
	console.log(age);
}
foo();
console.log(age);
```

The results are:
```
65
23
```

Because the first age is a local variable, but the second is a global one.


## 5. Scoping and the Scope Chain
### 5.1. Scoping in JavaScript
- Scoping answers the question “where can we access a certain variable?”
- **Each new function creates a scope**: the space/environment, in which the variables it defines are accessible.
- **Lexical scoping**: a function that is lexically within another function gets access to the scope of the outer function.

![Scoping in JavaScript](https://lh3.googleusercontent.com/F4IJgAKT-DtOdIqxYEgCzS_im4MhDRX2VjF87eQkppiqA0jH2B-_ILhjtd5GmkmvOofxfcFvLvCIKOqyPJ9lkgHmYdPQvuCVHDxzUgQJKe5v81RMU_Gzbqe018Erp2Q6z9dDNwICMctzdJsYnv9YM3nLgg255Qr-6Ml9zoR1moGZjQEDTAlPFIUxioSS_GNm41KYGaBp7A03Hp745fKCPJJ6vtZ2ko0PbFfs_Imxgo8bvxwtC6wuw9IwfynWhwJHnPhyVYFL4KpmHbzWnlBVQU9du6gCElBNNQnUUOnSyYAyVNfiRPYd7ifb2Oj8KUwFl73bJqVQ1JQNhipx0qFwbDfUqSo7Z8aF9CxWLBFyPvd6lKaZyBTVcUvMAHd5J4Fp9W3mZWOopCKzrBQIrN6O4vW7peoZEgEc-027t1wpln7pQZ-4EUOTb7tRxF0qnLwcTPxzFNFjne2gLiL9oQeOG9Uta12St74BqUM9eDKFv7fvzfERLjmvVE6j4WD0LwXaWt2e_12qjU3A4l-9z4FfsGUbUlbY5M-xcPIkXSJJSEaG3s_H9TG4LB1FPrbJIvrWzB9dR0LUKMYt4W2lNRtbFQwdLjc7CNBF4Z1nv1s5m9xEOWNX5be7ZXEKgh10WMSaHF2sNOPnxuiE7y9eRjXFhMtQtNQUIxRydVum7N4dKg=w1440-h560-no)

### 5.2. Execution Stack vs Scope Chain
Though the stack and scope chain look similar, they are still different.
![Execution Stack vs Scope Chain](https://lh3.googleusercontent.com/boB66Vu2o8EFG1Q8eWHzMDlCviauiFy2kX9ra0vi7TIg9-covb4qyOaz6sWgkukQlfhTl1eB-zeww6-wPd1aIhc6xdysxDFHeilC2VceCgfiPZfrhvvq7I4vErzy8kqbipEkFLRFH0w5jHseqzYpLf6dNJ5LZPNAv4FSrDSGMZ1Se1hHOP1xjfptBUqOANZjzgDqfSVNBjSzrxQIf7DJa25UUijwP24rZtxsVCU6gVO3qu1Z_KOzNsGMRKmL4SmAjW4DjtyBzCQEppanyCIJMubOtGZlQN3as2zZ2bDteFWtvJ_kKSMsRTP5Apu3W1bxEX0ABqy_POobuEsYCqKmlQyga6jt8ujUhFnpoQzJC_Gq4sdZ2-qAH4E5h48gUwFCS2HH-d1Q4zckCR4vs7C7EwGfrWVHYcaH0WUHnm43gav0xTenX_OwMKIHODWOkn76jJDdgMIHxSfIFJ_3vJPAe8sp_xp_KFQjwom9H5_s4Hk710hKjdaeyh_4mSrT2RVRZ1g5wUA2wO0d_DbKF-rlmt0qhPuO803sTzoIoPrAVcULzecG10ClbVSWhIh81IEkiZEXv-jCwuFt9UmpfjQlyTmiU7qeO1FRvUGC5294UGDtgNjCVpDbIPx8XbRsPHF2gr8ALfbkwVxIeqvamSjzzVD3eO47YX2n5tDTn1yIqg=w1440-h643-no)

```javaScript
var a = 'Hello!';
first();

function first() {
	var b = 'Hi';
	second();

	function second() {
		var c = 'Hey!';
		third();
	}
}

function third() {
	var d = 'John';
	console.log(c);
}

```

The execution result:
```log
Uncaught ReferenceError: c is not defined.
```

Because of the scope of the third function, it can only access variable a and d.

## 6. The ‘this’ Keyword
- **Regular function call**: the this keyword points at the global object, (the window object, in the browser).
- **Method call**: the this variable points to the object that is calling the method.

The this keyword is not assigned a value until a function where it is defined is actually called.

## 7. The ‘this’ Keyword in Practice

**Case 1**:
```javaScript

calculateAge(1985);

function calculateAge(year) {
	console.log(2016 - year);
	console.log(this); //First 'this'
}

var john = {
	name: 'John',
	yearOfBirth: 1990,
	calculateAge: function() {
		console.log(this); //Second 'this'
		console.log(2016 - this.yearOfBirth);
	}
}
john.calculateAge();
```

In this case, the first ‘this’ is the window object, and the second ‘this’ is the john object.

**Case 2**:
```javaScript
var john = {
	name: 'John',
	yearOfBirth: 1990,
	calculateAge: function() {
		console.log(this); //First 'this'
		console.log(2016 - this.yearOfBirth);
		function innerFunction() {
			console.log(this); //Second 'this'
		}
		innerFunction();
	}
}

john.calculateAge();
```

In this case, the first ‘this’ is the john object, however, the second object is  the window object. It’s because the second ‘this’ is inside a regular function call.

**Case 3 (Method Borrowing)**:
```javaScript
var john = {
	name: 'John',
	yearOfBirth: 1990,
	calculateAge: function() {
		console.log(this);
		console.log(2016 - this.yearOfBirth);
	}
}

john.calculateAge();

var mike = {
	name: 'Mike',
	yearOfBirth: 1984
}

mike.calculateAge = john.calculateAge;

```

In this case, ‘this’ in calling john.calculateAge() is john object, and ‘this’ in calling mike.calculateAge() is mike object.
