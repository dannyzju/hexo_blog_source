---
title: 'Put It All Together: The Budget App Project Part I'
date: 2017-05-28 11:14:49
tags:
- 学习笔记
- tech
- JavaScript
---

## 1. Project Planning and Architecture
### 1.1. Architecture Preview
The following is the final architecture preview:
![Architecture Preview](https://lh3.googleusercontent.com/eHN4cOiKul0fFzt9c-ZMWMbVQYnYH8cU7YbCz7ndP-a1TcZPksuWvwSZOAPnxBJVuZamnkmszAtyT-vOxOsBTUh-LsQ-Dy_PWtAFKBFPPYnHWmdv5JQ-nwBjhmCjOPL8T_eKDYXgvp1ho0rCFBH2BI71oqMEEEnBFQKlWEWD8NeHWpxFkdaVa-9adznp9o81pPsnL6ZAz6HBzDoXFagESydtpv6Rf1U6GTpw-pS-eBIumvtp5kwUh1s2dYxvNvMPG9ZcBkUOT-eFPJzc6p2pNPgA6uuNnR_m8r-0nYbOssjo0ObJdgm7POwyaRaZSuajsAlwRK3uTGlceWf_omICqZwpJJr2bm1LU9ZE2MHOHzUTdt6dWCnw-H-Ih8DAoh1k6ThidJ8q6-HybfsV5BiLwCzXL5-kaqPo5MB42aqy7tEMMu5uWBNyXoEfKVtINeSy1jsflW5RbUu3tMXApTUjxscymMur7P7xsUGYCQ_lTU9eylIDO-F6u7V7w88igzTXZIfXTZvbg1198X3BYYiuciWGTSo-4rGdMCVS_HfCoiNbY3bAjoc5ffRt0H738I9tVaylNwFiAJc0ZavF4YNb2QbZsJCmNU5ffZYfcC9hLDd63JJ-RYEZiQzpMG3MVlAyjfETp7EDZlHFulj9dfIBlJE3jOuEjTaEBO0dT-MHMw=w1177-h681-no)

But let's not to be so fast, next we'll start planning from scratch.

### 1.2. Planning
![Planning](https://lh3.googleusercontent.com/Vq_20C_jNjPPcLjLnSgvcWKrCMhaCK9X1OuTr4iQp1P9P0tvqvnVzBRAUUR4ciMczOG3EySVrrh40T92yNVS9JQRIfmjGLIwLmC5GsjvdMx-HhmP6BHobjv-ksFax6jAyYcYb_tD0EqKYS0UlXQzy606iJqsMYTdVDY9AVc03L5iBf0F_zwalbFPAuyByUj1PabHhRX976zPxOdWqVKYt3DBAp-GPMHRi-uiZ2G4ApX-XaLVgVooOtOXVo1-4-ZyqpOkJZIUK1WdZh6i52YwEsih--r6t6tbHCkkxpDfRZGrMyg3YdU0-VH3Vo4sE3sHka1Uk6HmlluA20Pqw0SdWS1EwV_KNsLsRBF4mkhlTkYggHbB7E4JosBIcbeSOtJ_1q_u-_7X_jI-2lL2kE8PVowlPQa4QxEJ08P6t2dRoRJd6H5DbTd1IZ_O30HMfMdnsaX8Y-YgpIXt0VIZIk_KVz_C7mxn3qQhxkj2rEKw8QIcsAIQFOPrOwCdOGNA18sT_gGmVElSoVHlfz7Hn8w4wuhQztqL3zJpu4YGYajg80QnqSyQ-rHt8wAEvqb3FeTz3JG8tnXOpEyTI6Wd0RxgD5XBBmMsxs8pZJcH2fNdeGDVNIRcKwD6cb79qmFP-pEo6Hi1N48_dx7OKcR0AXOMnHpTaaHZYFDQy_PMZJwo3A=w1177-h556-no)

### 1.3. Structuring Our Code with Modules

- **`Modules`**
	- Important aspect of any robust application's architecture;
	- Keep the units of code for a project both cleanly separated and organized;
	- Encapsulate some data into privacy and expose other data publicly.


![Structuring Out Code with Modules](https://lh3.googleusercontent.com/_WJUZnWVNk1q-KifAlnOMyeTt0V-nRCciTWBTR6eKtBLUlTvFG8dGIFQI2yoPtPg35jDFkTt5w9fR1UTdou1o-gNLveHAUldxUr5KwkRolnRpx3VzatRIO7Z7k-dSGsBgK-IuJgV99Sp2lvfDHxy-Js6-fKx2o3PyM8iVC5rT3UvLpg1fJ5HDeOOeC64GdPJ4woBZDGUY5OsZBJ6lYHMDMQDCWGriULwHiItzxjDJAKKWmEMprFVJqk85j0nsRaIbqixK-BQ-ep6GEkiECAurrTEgs1LNFhdhFcXGJoTPvDwiHSUVufzkZxb9LndkNBibo9zwd6RJH8X8U70jgOG9aYArOOlIUYI53Za4G0hue2Lx9onMXg-FI3WbrshVyfFtPDx4fqnwVGsfEpZKfLxYtYSZiE0-6WbAOzHLKYT90L1vK7JFZGZwQWrtYPG_AdJw9q8cstjE2vRhhYHinOuiv2Z6GgWlgk_ysTfv-h1yaZf0-Q_rGVngwgpqb7-A-uqD3czOQ0cw2oT0YDTpMk0Zrv-DpI5Fi5cc6wC5hgy-dVkRHmvf2mVmyK384mueQpAekJJjYMogmml0z6EZEhPJctMuAjX6d7p-Xkg13eEw9Z1U83cx7H0ZVY6Tycxd4WpLggutzf330rRc8egouvNoD5xEJSYEZTl_YMkZHDNaQ=w1177-h825-no)

## 2. Implementing the Module Pattern

- **`What you will learn in this section:`**
  - How to use the module pattern;
  - More about private and public data, encapsulation and separation of concerns.

### 2.1. Data Encapsulation Module
```java
var budgetController = (function() {
	var x = 23;
	var add = function(a) {
		return x + a;
	}

	return {
		publicTest: function(b) {
			console.log(add(b));
		}
	}
})();
```
Running Result:

![Data Encapsulation Module Running Result](https://lh3.googleusercontent.com/y4awh7GXtZWU6VMC6-nW-I8ZfYz2Pkt1WaGojFihXUPMhR3M8Z1b815sUCZxtQcWqgF8lHFIPIxBR1_4_qOdr64XSobxXfbOXtPQDYadpwoFM3DCOss4HH4N-_zZrw-9TWmKBHe3qoLDUaEiLfZZLq5-I2xm3zoFqe9m7JjHzuuNRiPtYUfV9zM0A8JAK4MisQx7Qjj2cCE8zF28BXnZl9Zc4oMZtemx3ynQJGPjSbkro51AvzTuNEFkmp7i6xt-YfHpdZeAX63ye2jOdxtqEWdT2a0HonHJyTXM-7Nlx2LT32HhxvNJlRsoFNELIii8PQe0bcT0jOnSU0XjthHJ27muQ856c5xN5IX4sNw_6TSfRYr53n2ikIjvc28X9pOzBpeYL4rdRe_vOrKt9Wr4KHliJzcOaipVgaadHQiZNCQIUVAfh7rUk2zRQI0mvJnwuBLysaJNyfTdDZMag8bADBoQd3M38XKwZVyUeh9pAiGZGZqeUg8ELwArGjnIwWv8wZ22hi_qiq0jQkbS4FOvwHh2dbvA5mTdlpsRFdN5484Bz-IYibEUYM_TLw9X8rb7VPQfoeZXjhMwAaLjQkkoFmGAOLK5S9k11il-lhF_LLV91io5Wj1J52OUZzFZ6ASwoT9MQ_vsFP8jVZekxPxnfZFifCHMo11ThEuPllwyBQ=w1734-h232-no)


### 2.2. UI Controller

```java
// BUDGET CONTROLLER
var budgetController = (function() {
	var x = 23;
	var add = function(a) {
		return x + a;
	}

	return {
		publicTest: function(b) {
			return add(b);
		}
	}
})();

// UI CONTROLLER
var UIController = (function() {
	// Some code
})();

// GLOBAL APP CONTROLLER
var controller = (function(budgetCtrl, UICtrl) {
	var z = budgetCtrl.publicTest(5);
	return {
		anotherPublic: function() {
			console.log(z);
		}
	}
})(budgetController, UIController);
```


## 3. Setting up the First Event Listeners

- **`What you will learn in this section:`**
  - How to set up event listeners for keypress events
  - How to use event object

```java
// BUDGET CONTROLLER
var budgetController = (function() {
	// Some code
})();

// UI CONTROLLER
var UIController = (function() {
	// Some code
})();

// GLOBAL APP CONTROLLER
var controller = (function(budgetCtrl, UICtrl) {

	var ctrlAddItem = function() {
		// 1. Get the field input data
		// 2. Add the item to the budget controller
		// 3. Add the item to the UI
		// 4. Calculate the budget
		// 5. Display the budget on the UI
		console.log("It works.");
	}
	document.querySelector('.add_btn').addEventListener('click', ctrlAddItem);

	document.addEventListener('keypress', function(event)) {
		console.log(event);
		if (event.keyCode === 13 || event.which === 13) {
			console.log('ENTER was pressed.');
			ctrlAddItem();
		}
	}
})(budgetController, UIController);
```

Reference:
- [JavaScript Event reference /MDN](https://developer.mozilla.org/en-US/docs/Web/Events)
- [Keycode Reference](http://keycodes.atjayjo.com)

## 4. Reading Input Data

- **`What you will learn in this section:`**
  - How to read data from different HTML input types;

```javaScript
// UI CONTROLLER
var UIController = (function() {
	var DOMstrings = {
		inputType: '.add__type',
		inputDescription: '.add_description',
		inputValue: '.add__value'
	};


	return {
		getInput: function() {
			return {
			var type = document.querySelector(DOMstrings.inputType).value,
			var description = document.querySelector(DOMstrings.inputDescription).value,
			var value = document.querySelector(DOMstrings.inputValue).value
			};
		},
		getDOMstrings: function() {
			return DOMstrings;
		}
	};
})();

// GLOBAL APP CONTROLLER
var controller = (function(budgetCtrl, UICtrl) {
	var DOM = UICtrl.getDOMstrings();

	var ctrlAddItem = function() {
		// 1. Get the field input data
		var input = UICtrl.getInput();
		console.log(input);

		// 2. Add the item to the budget controller
		// 3. Add the item to the UI
		// 4. Calculate the budget
		// 5. Display the budget on the UI
		console.log("It works.");
	}
	document.querySelector(DOM.inputBtn).addEventListener('click', ctrlAddItem);

	document.addEventListener('keypress', function(event)) {
		console.log(event);
		if (event.keyCode === 13 || event.which === 13) {
			console.log('ENTER was pressed.');
			ctrlAddItem();
		}
	}
})(budgetController, UIController);

```

## 5. Creating an Initialization Function

- **`What you will learn in this section:`**
  - How and why to create an initialization function.

```javaScript
// GLOBAL APP CONTROLLER
var controller = (function(budgetCtrl, UICtrl) {
	var setupEventListners = function() {
	var DOM = UICtrl.getDOMstrings();
	document.querySelector(DOM.inputBtn).addEventListener('click', ctrlAddItem);

	document.addEventListener('keypress', function(event) {
		console.log(event);
		if (event.keyCode === 13 || event.which === 13) {
			console.log('ENTER was pressed.');
			ctrlAddItem();
		}
	});
	};

	var ctrlAddItem = function() {
		// 1. Get the field input data
		var input = UICtrl.getInput();
		console.log(input);

		// 2. Add the item to the budget controller
		// 3. Add the item to the UI
		// 4. Calculate the budget
		// 5. Display the budget on the UI
		console.log("It works.");
	};

	return {
		init: function() { //Our public init method
			console.log('Application has started.');
			setupEventListeners();
		}
	}

})(budgetController, UIController);

```

## 6. Creating Income and Expense Function Constructors

- **`What you will learn in this section:`**
  - How to choose function constructors that meet our application's needs;
  - How to set up a proper data structure for our budget controller.

```javaScript

// BUDGET CONTROLLER
var budgetController = (function() {
	// Some code
	var Expense = function(id, description, value) {
		this.id = id;
		this.description = description;
		this.value = value;
	};

	var Income = function(id, description, value) {
		this.id = id;
		this.description = description;
		this.value = value;
	};

	var data = {
		allItems: {
			exp: [],
			inc: []
		},
		totals: {
			exp: 0,
			inc: 0
		}
	}
})();

```


## 7. Adding a New Item to Our Budget Controller

- **`What you will learn in this section:`**
  - How to avoid conflicts in our data structures;
  - How and why to pass data from one module to another.

```javaScript

// BUDGET CONTROLLER
var budgetController = (function() {
	// Some code
	var Expense = function(id, description, value) {
		this.id = id;
		this.description = description;
		this.value = value;
	};

	var Income = function(id, description, value) {
		this.id = id;
		this.description = description;
		this.value = value;
	};

	var data = {
		allItems: {
			exp: [],
			inc: []
		},
		totals: {
			exp: 0,
			inc: 0
		}
	};

	return {
		addItem: function(type, des, val) {
			var newItem, ID;
			//Create new ID
			ID = 0;
			if (data.allItems[type].length > 0) {
				ID = data.allItems[type][data.allItems[type].length - 1].id + 1;
			} else {
				ID = 0;
			}

			// Create new item based on 'inc' or 'exp' type
			if (type === 'exp') {
				newItem = new Expense(ID, des, val);
			} else if (type === 'inc') {
				newItem = new Income(ID, des, val);
			}

			//Push it into our data structure
			data.allItems[type].push(newItem);

			//Return the new element
			return newItem;
		},
		testing: function() {
			console.log(data);
		}
	};

})();


// GLOBAL APP CONTROLLER
var controller = (function(budgetCtrl, UICtrl) {
	var setupEventListners = function() {
	var DOM = UICtrl.getDOMstrings();
	document.querySelector(DOM.inputBtn).addEventListener('click', ctrlAddItem);

	document.addEventListener('keypress', function(event) {
		console.log(event);
		if (event.keyCode === 13 || event.which === 13) {
			console.log('ENTER was pressed.');
			ctrlAddItem();
		}
	});
	};

	var ctrlAddItem = function() {
		var input, newItem;

		// 1. Get the field input data
		input = UICtrl.getInput();
		console.log(input);

		// 2. Add the item to the budget controller
		newItem = budgetCtrl.addItem(input.type, input.description, input.value);

		// 3. Add the item to the UI
		// 4. Calculate the budget
		// 5. Display the budget on the UI
		console.log("It works.");
	};

	return {
		init: function() { //Our public init method
			console.log('Application has started.');
			setupEventListeners();
		}
	}

})(budgetController, UIController);

```


## 8. Adding a New Item to the UI

- **`What you will learn in this section:`**
  - A technique for adding big chunks of HTML into the DOM;
  - How to replace parts of strings;
  - How to do DOM manipulation using the insertAdjacentHTML method.

```javaScript
// UI CONTROLLER
var UIController = (function() {
	var DOMstrings = {
		inputType: '.add__type',
		inputDescription: '.add_description',
		inputValue: '.add__value'，
		inputBtn: '.add_btn',
		incomeContainer: '.income__list',
		expensesContainer: '.expenses__list'
	};

	return {
		getInput: function() {
			return {
			var type = document.querySelector(DOMstrings.inputType).value,
			var description = document.querySelector(DOMstrings.inputDescription).value,
			var value = document.querySelector(DOMstrings.inputValue).value
			};
		},

		addListItem: function(obj, type) {
			var html, newHtml, element;
			// Create HTML string with placeholder text

			if (type === 'inc') {
        element = DOMstrings.incomeContainer;

        html = '<div class="item clearfix" id="inc-%id%"> <div class="item__description">%description%</div><div class="right clearfix"><div class="item__value">%value%</div><div class="item__delete"><button class="item__delete--btn"><i class="ion-ios-close-outline"></i></button></div></div></div>';
    } else if (type === 'exp') {
        element = DOMstrings.expensesContainer;

        html = '<div class="item clearfix" id="exp-%id%"><div class="item__description">%description%</div><div class="right clearfix"><div class="item__value">%value%</div><div class="item__percentage">21%</div><div class="item__delete"><button class="item__delete--btn"><i class="ion-ios-close-outline"></i></button></div></div></div>';
    }

			// Replace the placeholder text with some actual data
			newHtml = html.replace('%id%', obj.id);
			newHtml = newHtml.replace('%description%', obj.description);
			newHtml = newHtml.replace('%value%', obj.value);

			// Insert the HTML into the DOM
			document.querySelector(element).insertAdjacentHTML('beforeend', newHtml);
		},

		getDOMstrings: function() {
			return DOMstrings;
		}
	};
})();

// GLOBAL APP CONTROLLER
var controller = (function(budgetCtrl, UICtrl) {
	var setupEventListners = function() {
	var DOM = UICtrl.getDOMstrings();
	document.querySelector(DOM.inputBtn).addEventListener('click', ctrlAddItem);

	document.addEventListener('keypress', function(event) {
		console.log(event);
		if (event.keyCode === 13 || event.which === 13) {
			console.log('ENTER was pressed.');
			ctrlAddItem();
		}
	});
	};

	var ctrlAddItem = function() {
		var input, newItem;

		// 1. Get the field input data
		input = UICtrl.getInput();
		console.log(input);

		// 2. Add the item to the budget controller
		newItem = budgetCtrl.addItem(input.type, input.description, input.value);

		// 3. Add the item to the UI
		UICtrl.addListItem(newItem, input.type);

		// 4. Calculate the budget
		// 5. Display the budget on the UI
		console.log("It works.");
	};

	return {
		init: function() { //Our public init method
			console.log('Application has started.');
			setupEventListeners();
		}
	}

})(budgetController, UIController);
```

## 9. Clearing Our Input Fields

- **`What you will learn in this section:`**
  - How to clear HTML fields;
  - How to use querySelectorAll;
  - How to convert a list to an array;
  - A better way to loop over an array then for loops: for each

```javaScript

// UI CONTROLLER
var UIController = (function() {
	var DOMstrings = {
		inputType: '.add__type',
		inputDescription: '.add_description',
		inputValue: '.add__value'，
		inputBtn: '.add_btn',
		incomeContainer: '.income__list',
		expensesContainer: '.expenses__list'
	};


	return {
		getInput: function() {
			return {
			var type = document.querySelector(DOMstrings.inputType).value,
			var description = document.querySelector(DOMstrings.inputDescription).value,
			var value = document.querySelector(DOMstrings.inputValue).value
			};
		},

		addListItem: function(obj, type) {
			var html, newHtml, element;
			// Create HTML string with placeholder text

			if (type === 'inc') {
        element = DOMstrings.incomeContainer;

        html = '<div class="item clearfix" id="inc-%id%"> <div class="item__description">%description%</div><div class="right clearfix"><div class="item__value">%value%</div><div class="item__delete"><button class="item__delete--btn"><i class="ion-ios-close-outline"></i></button></div></div></div>';
    } else if (type === 'exp') {
        element = DOMstrings.expensesContainer;

        html = '<div class="item clearfix" id="exp-%id%"><div class="item__description">%description%</div><div class="right clearfix"><div class="item__value">%value%</div><div class="item__percentage">21%</div><div class="item__delete"><button class="item__delete--btn"><i class="ion-ios-close-outline"></i></button></div></div></div>';
    }

			// Replace the placeholder text with some actual data
			newHtml = html.replace('%id%', obj.id);
			newHtml = newHtml.replace('%description%', obj.description);
			newHtml = newHtml.replace('%value%', obj.value);

			// Insert the HTML into the DOM
			document.querySelector(element).insertAdjacentHTML('beforeend', newHtml);
		},

		clearFields: function() {
			var fields;

			fields = document.querySelectorAll(DOMstrings.inputDescription + ', ' + DOMstrings.inputValue);

			var fieldsArr = Array.prototype.slice.call(fields);  

			fieldsArr.forEach(function(current, index, array) {
				current.value = "";
			});

			fieldsArr[0].focus();
		},

		getDOMstrings: function() {
			return DOMstrings;
		}
	};
})();


// GLOBAL APP CONTROLLER
var controller = (function(budgetCtrl, UICtrl) {
	var setupEventListners = function() {
	var DOM = UICtrl.getDOMstrings();
	document.querySelector(DOM.inputBtn).addEventListener('click', ctrlAddItem);

	document.addEventListener('keypress', function(event) {
		console.log(event);
		if (event.keyCode === 13 || event.which === 13) {
			console.log('ENTER was pressed.');
			ctrlAddItem();
		}
	});
	};

	var ctrlAddItem = function() {
		var input, newItem;

		// 1. Get the field input data
		input = UICtrl.getInput();
		console.log(input);

		// 2. Add the item to the budget controller
		newItem = budgetCtrl.addItem(input.type, input.description, input.value);

		// 3. Add the item to the UI
		UICtrl.addListItem(newItem, input.type);

		// 4. Clear the fields
		UICtrl.clearFields();

		// 4. Calculate the budget
		// 5. Display the budget on the UI
		console.log("It works.");
	};

	return {
		init: function() { //Our public init method
			console.log('Application has started.');
			setupEventListeners();
		}
	}

})(budgetController, UIController);

```

## 10. Updating the Budget: Controller

- **`What you will learn in this section:`**
  - How to convert field inputs to numbers;
  - How to prevent false inputs

To convert a string to a number, we can use parseFloat.

```javaScript
		getInput: function() {
			return {
			var type = document.querySelector(DOMstrings.inputType).value,
			var description = document.querySelector(DOMstrings.inputDescription).value,
			var value = parseFloat(document.querySelector(DOMstrings.inputValue).value)
			};
		},
```

Apply DRY and prevent false inputs
```javaScript
// GLOBAL APP CONTROLLER
var controller = (function(budgetCtrl, UICtrl) {
	var setupEventListners = function() {
	var DOM = UICtrl.getDOMstrings();
	document.querySelector(DOM.inputBtn).addEventListener('click', ctrlAddItem);

	document.addEventListener('keypress', function(event) {
		console.log(event);
		if (event.keyCode === 13 || event.which === 13) {
			console.log('ENTER was pressed.');
			ctrlAddItem();
		}
	});
	};

	var updateBudget = function() {
		// 1. Calculate the budget
		// 2. Return the budget
		// 3. Display the budget on the UI

	};

	var ctrlAddItem = function() {
		var input, newItem;

		// 1. Get the field input data
		input = UICtrl.getInput();
		console.log(input);

		if (input.description !== "" && !isNaN(input.value) && input.value > 0)  {
			// 2. Add the item to the budget controller
			newItem = budgetCtrl.addItem(input.type, input.description, input.value);

			// 3. Add the item to the UI
			UICtrl.addListItem(newItem, input.type);

			// 4. Clear the fields
			UICtrl.clearFields();

			// 5. Calculate and update budget
			updateBudget();
		}
	};

	return {
		init: function() { //Our public init method
			console.log('Application has started.');
			setupEventListeners();
		}
	}

})(budgetController, UIController);

```


## 11. Updating the Budget: Budget Controller

- **`What you will learn in this section:`**
  - How and why to create simple, reusable functions with only one purpose;
  - How to sum all elements of an array using the forEach method.

```javaScript

// BUDGET CONTROLLER
var budgetController = (function() {
	// Some code
	var Expense = function(id, description, value) {
		this.id = id;
		this.description = description;
		this.value = value;
	};

	var Income = function(id, description, value) {
		this.id = id;
		this.description = description;
		this.value = value;
	};

	var calculateTotal = function(type) {
		var sum = 0;
		data.allItems[type].forEach(function(cur) {
			sum = sum + cur.value;
		});
		data.totals[type] = sum;
	};

	var data = {
		allItems: {
			exp: [],
			inc: []
		},
		totals: {
			exp: 0,
			inc: 0
		},
		budget: 0,
		percentage: -1
	};

	return {
		addItem: function(type, des, val) {
			var newItem, ID;
			//Create new ID
			ID = 0;
			if (data.allItems[type].length > 0) {
				ID = data.allItems[type][data.allItems[type].length - 1].id + 1;
			} else {
				ID = 0;
			}

			// Create new item based on 'inc' or 'exp' type
			if (type === 'exp') {
				newItem = new Expense(ID, des, val);
			} else if (type === 'inc') {
				newItem = new Income(ID, des, val);
			}

			//Push it into our data structure
			data.allItems[type].push(newItem);

			//Return the new element
			return newItem;
		},

		calculateBudget: function() {
			// calculate total income and expenses
			calculateTotal('exp');
			calculateTotal('inc');
			// Calculate the budget: income - expenses
			data.budget = data.totals.inc - data.totals.exp;

			// Calculate the percentage of income that we spent
			if (data.totals.inc > 0) {
				data.percentage = Math.round((data.totals.exp / data.totals.inc) * 100);
			} else {
				data.percentage = -1;
			}
		},

		getBudget: function() {
			return {
				budget: data.budget,
				totalInc: data.totals.inc,
				totalExp: data.totals.exp,
				percentage: data.percentage
			};
		},

		testing: function() {
			console.log(data);
		}
	};

})();
```

In updateBudget method:

```javaScript
...
	var updateBudget = function() {
		// 1. Calculate the budget
		budgetCtrl.calculateBudget();
		// 2. Return the budget
		var budget = bubdgetctrl.getBudget();
		// 3. Display the budget on the UI
		console.log(budget);
	};
...
```


## 12. Updating the Budget: UI Controller

- **`What you will learn in this section:`**
  - Practice DOM manipulation by updating the budget and total values.

```javaScript

// UI CONTROLLER
var UIController = (function() {
	var DOMstrings = {
		inputType: '.add__type',
		inputDescription: '.add_description',
		inputValue: '.add__value'，
		inputBtn: '.add_btn',
		incomeContainer: '.income__list',
		expensesContainer: '.expenses__list',
		budgetLabel: '.budget__value',
		incomeLabeL: '.budget__income--value',
		expensesLabel: '.budget__expenses--value',
		percentageLabel: '.budget__expenses--percentage'
	};


	return {
		getInput: function() {
			return {
			var type = document.querySelector(DOMstrings.inputType).value,
			var description = document.querySelector(DOMstrings.inputDescription).value,
			var value = document.querySelector(DOMstrings.inputValue).value
			};
		},

		addListItem: function(obj, type) {
			var html, newHtml, element;
			// Create HTML string with placeholder text

			if (type === 'inc') {
        element = DOMstrings.incomeContainer;

        html = '<div class="item clearfix" id="inc-%id%"> <div class="item__description">%description%</div><div class="right clearfix"><div class="item__value">%value%</div><div class="item__delete"><button class="item__delete--btn"><i class="ion-ios-close-outline"></i></button></div></div></div>';
    } else if (type === 'exp') {
        element = DOMstrings.expensesContainer;

        html = '<div class="item clearfix" id="exp-%id%"><div class="item__description">%description%</div><div class="right clearfix"><div class="item__value">%value%</div><div class="item__percentage">21%</div><div class="item__delete"><button class="item__delete--btn"><i class="ion-ios-close-outline"></i></button></div></div></div>';
    }

			// Replace the placeholder text with some actual data
			newHtml = html.replace('%id%', obj.id);
			newHtml = newHtml.replace('%description%', obj.description);
			newHtml = newHtml.replace('%value%', obj.value);

			// Insert the HTML into the DOM
			document.querySelector(element).insertAdjacentHTML('beforeend', newHtml);
		},

		clearFields: function() {
			var fields;

			fields = document.querySelectorAll(DOMstrings.inputDescription + ', ' + DOMstrings.inputValue);

			var fieldsArr = Array.prototype.slice.call(fields);  

			fieldsArr.forEach(function(current, index, array) {
				current.value = "";
			});

			fieldsArr[0].focus();
		},

		displayBudget: function(obj) {
			document.querySelector(DOMstrings.budgetLabel).textContent = obj.budget;
			document.querySelector(DOMstrings.incomeLabel).textContent = totoalInc;
			document.querySelector(DOMstrings.expensesLabel).textContent = totalExp;

			if（obj.percentage > 0）{
				document.querySelector(DOMstrings.percentageLabel).textContent = percentage + '%';
			} else {
			 document.querySelector(DOMstrings.percentageLabel).textContent = '---';
			}
		},

		getDOMstrings: function() {
			return DOMstrings;
		}
	};
})();

// GLOBAL APP CONTROLLER
var controller = (function(budgetCtrl, UICtrl) {
	var setupEventListners = function() {
	var DOM = UICtrl.getDOMstrings();
	document.querySelector(DOM.inputBtn).addEventListener('click', ctrlAddItem);

	document.addEventListener('keypress', function(event) {
		console.log(event);
		if (event.keyCode === 13 || event.which === 13) {
			console.log('ENTER was pressed.');
			ctrlAddItem();
		}
	});
	};

	var updateBudget = function() {
		// 1. Calculate the budget
		budgetCtrl.calculateBudget();
		// 2. Return the budget
		var budget = bubdgetctrl.getBudget();
		// 3. Display the budget on the UI
		console.log(budget);
	};

	var ctrlAddItem = function() {
		var input, newItem;

		// 1. Get the field input data
		input = UICtrl.getInput();
		console.log(input);

		if (input.description !== "" && !isNaN(input.value) && input.value > 0)  {
			// 2. Add the item to the budget controller
			newItem = budgetCtrl.addItem(input.type, input.description, input.value);

			// 3. Add the item to the UI
			UICtrl.addListItem(newItem, input.type);

			// 4. Clear the fields
			UICtrl.clearFields();

			// 5. Calculate and update budget
			updateBudget();
		}
	};

	return {
		init: function() { //Our public init method
			console.log('Application has started.');
			UICtrl.displayBudget({
				budget: 0,
				totalInc: 0,
				totalExp: 0,
				percentage: -1
			});
			setupEventListeners();
		}
	}

})(budgetController, UIController);

```
