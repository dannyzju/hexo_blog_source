---
title: 'Put It All Together: The Budget App Project: Part III'
date: 2017-06-25 11:44:13
tags:
- 学习笔记
- tech
- JavaScript
---

## 1. Project Planning and Architecture: Step 3
### 1.1. What We Just Completed
![What We Just Completed](https://lh3.googleusercontent.com/zcQMdq5e9yHiXSsAr5CZAF4vlKBZV11aGMZjd2Tec3o-nkJhKLOIIihcwA_DebCHNEJtMu_3EFPHmCpPQ7O666yAV4y9Ab2XrxWfUg3g9lQW1n6oqijQW6OzhW5dWrC63FgSEcf7Ef6UbVclr5gvxgwTDyKuBMQEflW1lhefF_BsRFR1vHD6Gsks8ZRFlmmlcnx_k80q782tXrSElmjqifgZCpEY5bPPt8o8K5CBk5I5eCovsGuYqzPp7h46Km-crJ5t-f6sjNmeeBHdsQ-O-uFYZXUmAsgnc_i7W2MWj4u57usg4CSN0H3yH98hV2SgebkUqn6HRlIwo78oPLef8qniBQLLibWFhYAfhLGoMqzQkFd2383JPDlSqJZ0MEHf6F4YmpVea_e7Vb3U0u6AhYa3C0X-GPF0yWbxtoyMi97Z-W12-n7QFUNQWen4kGOXAnipezTUfmeRGFA7BVsLLyLi3bkfWbKoAkyPOv5qAsdkLV1pOUEewm0BW8dGjmawiyVRUvseY1wq8m7OToWGTq92aM6FhWTosG3krgCPCNLI62lTXgFgwjK7yRV_5Jnf0iVqbqGwlXRQMCWlEPU1jwmoF5BnXossg4yBM7AVd0f5lMEXvSfOEZFKuTJdX6m2tP6w3L-2-KAATJL8ioHK1MhNYmBCcwRONKZnGERIwA=w1592-h928-no)

### 1.2. Panning: Step 3
![Panning: Step 3](https://lh3.googleusercontent.com/iptcVLukbH-GpmuPlC7HORZ2rVsk_VEd9LCz8EkjKakE4658ijEZF-F8IBLVOfvWdoUYiXRhyCk8etI9MwzUxlj0DHX973A7eUbGOyj0nYJKmsEcKrYGztnWwC3XdGj2o-kBdtTKlOI1SdoZ4XSIQwvwSKszvE41tDTAzg7FrTuN8BwgAUolG2ojL75AVhkTpMHtEbtXx3XgMNBDQkddsXhkKPamv7sdEas2vBd9rS3IBuV8OE_68qdJOV3toEtabpfIGjsfrYuQWlDBevZ9RgONmySfDad9bFfLE3eSCX8L956wqS992mX7hU3EwJWlFQtH2qatXnPDuD9-2PeTdbWRKlRFDckD9-HtxdogNQsne9Kvmq8Q7I9jykIiWVUT_Yn0OaWPvBAN1l8ExOHLrYENuTuQRxZEldKoqfM4pSNAzPkO3dxLRCms3psFVgMVVrnuCo2yC6WC4M4rzenPLN__h0fMLggeeDZby5HTRqUjH8QwH8mDuPqKbqfQ9Si_TBTXB2jDW-FqGtvJOSQECKBxJrHt2AEr1h7Tw8sxWYptjyrYkoIJpWLW6BqM_UVBCLvdVuWOLUBR5cEdC6EPasKUwUNyTF_QuxPG5UAtLZ-RDtHDyvaFlR0vwi99YIN1Py14TYuqeijjM47N00RJQIkIwEVjFvWN-l8WzcQp9g=w1704-h834-no)

## 2. Updating the Percentages: Controller
- What you will learn in this section:
	- Reinforcing the concepts and techniques we have learned so far.

Add updatePercentage Method in app controller.

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

		document.querySelector(DOM.container).addEventListener('click', ctrlDeleteItem);

	};

	var updateBudget = function() {
		// 1. Calculate the budget
		budgetCtrl.calculateBudget();
		// 2. Return the budget
		var budget = bubdgetctrl.getBudget();
		// 3. Display the budget on the UI
		console.log(budget);
	};

	var updatePercentages = function() {

		// 1. Calculate percentages
		// 2. Read percentages from the budget controller

		// 3. Update the UI with the new percentages


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

			// 6. Calculate and update percentage
			updatePercentages();
		}
	};

	var ctrlDeleteItem = function(event) {
		console.log(event.target);
		var itemID, splitID;
		itemID = event.target.parentNode.parentNode.parentNode.parentNode.id;
		if (itemID) {
			//inc-1
			splitID = itemID.split("-");
			type = splitID[0];
			ID = splitID[1];

			// 1. delete the item from the data structure
			budgetCtrl.deleteItem(type, ID);

			// 2. Delete the item from the UI
			UICtrl.deleteListItem(itemID);

			// 3. Update and show the new budget
			updateBudget();

			// 4. Calculate and update percentage
			updatePercentages();
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


## 3. Updating the Percentages: Budget Controller
- What you will learn in this lecture
	- How to make our budget controller interact with the Expense prototype.

```javaScript

// BUDGET CONTROLLER
var budgetController = (function() {
	// Some code
	var Expense = function(id, description, value) {
		this.id = id;
		this.description = description;
		this.value = value;
		this.percentage = -1;
	};

	Expense.prototype.calcPercentage = function(totalIncome) {
		if (totalIncome > 0) {
			this.percentage = Math.round((this.value / totalIncome) * 100);
		} else {
			this.percentage = -1;
		}
	};

	Expense.prototype.getPercentage = function() {
		return this.percentage;
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

		deleteItem: function(type, id) {
			var ids, index;
			// id = 3
			var ids = data.allItems[type].map(function(current) {
				return current.id;
			});

			index = ids.indexOf(id);
			if (index !=== -1) {
				data.allItems[type].splice(index, 1);
			}

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

		calculatePercentages: function() {
			data.allItems.exp.forEach(fuction(cur) {
				cur.calcPercentage(data.totals.inc);
			});
		},

		getPercentages: function() {
			var allPerc = data.allItems.exp.map(function(cur) {
				return cur.getPercentage();
			});
			return allPerc;
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


Now we can update our app controller:

```javaScript

	var updatePercentages = function() {
		// 1. Calculate percentages
		budgetCtrl.calculatePercentages();

		// 2. Read percentages from the budget controller
		var percentages = budgetCtrl.getPercentages();

		// 3. Update the UI with the new percentages
		console.log(percentages);

	};
```

## 4. Updating the Percentages: UI Controller
- What you will learn in this section:
	- How to create our own forEach function but for nodeLists instead of arrays.

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
		percentageLabel: '.budget__expenses--percentage',
		container: '.container',
		expensesPercLabel: '.item__percentage'
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

		deleteListItem: function(selectorID) {
			var el = document.getElementById(selectorID);
			el.parentNode.removeChild(el);
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

		displayPercentages: function(percentages) {
			var fields = document.querySelectorAll(DOMstrings.expensesPercLabel);
			var nodeListForEach = function(list, callback) {
				for (var i = 0; i < list.length; i++) {
					callback(list[i], i);
				}
			};

			nodeListForEach(fields, function(current, index) {
				if (percentages[index] > 0) {
					current.textContent = percentages[index] + "%";
				} else {
					current.textContent = '---';
				}
			});
		},

		getDOMstrings: function() {
			return DOMstrings;
		}
	};
})();

```


## 5. Formatting Our Budget Numbers: String Manipulation
- What you will learn in this lecture
	- How to use different String methods to manipulate strings.

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
		percentageLabel: '.budget__expenses--percentage',
		container: '.container',
		expensesPercLabel: '.item__percentage'
	};

	var formatNumber = function(num, type) {
			/*
			+ or - before number exactly 2 decimal points
			comma separating the thousands

			2310.4567 => + 2,310.46
			2000 -> + 2,000.00
			*/

			num = Math.abs(num);
			num = num.toFixed(2);
			numSplit = num.split('.');
			int = numSplit[0];
			if (int.length > 3) {
				int = int.substr(0, int.length - 3) + ',' + int.substr(int.length - 3, 3);
			}
			dec = numSplit[1];
			type === 'exp' ? sign = '-' : sign = '+';
			return type + ' ' + int + '.' + dec;
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
			newHtml = newHtml.replace('%value%', formatNumber(obj.value, type));

			// Insert the HTML into the DOM
			document.querySelector(element).insertAdjacentHTML('beforeend', newHtml);
		},

		deleteListItem: function(selectorID) {
			var el = document.getElementById(selectorID);
			el.parentNode.removeChild(el);
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
			var type;
			obj.budget > 0 ? type = 'inc' : type = 'exp';
			document.querySelector(DOMstrings.budgetLabel).textContent = formatNumber(obj.budget, type);
			document.querySelector(DOMstrings.incomeLabel).textContent = formatNumber(totoalInc, 'inc');
			document.querySelector(DOMstrings.expensesLabel).textContent = formatNumber(totalExp, 'exp');

			if（obj.percentage > 0）{
				document.querySelector(DOMstrings.percentageLabel).textContent = percentage + '%';
			} else {
			 document.querySelector(DOMstrings.percentageLabel).textContent = '---';
			}
		},

		displayPercentages: function(percentages) {
			var fields = document.querySelectorAll(DOMstrings.expensesPercLabel);
			var nodeListForEach = function(list, callback) {
				for (var i = 0; i < list.length; i++) {
					callback(list[i], i);
				}
			};

			nodeListForEach(fields, function(current, index) {
				if (percentages[index] > 0) {
					current.textContent = percentages[index] + "%";
				} else {
					current.textContent = '---';
				}
			});
		},

		getDOMstrings: function() {
			return DOMstrings;
		}
	};
})();

```

## 6. Displaying the Current Month and Year
- What you will learn in this lecture:
	- How to get the current date by using the Date object constructor.


Step1: add displayMonth function in UI controller

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
		percentageLabel: '.budget__expenses--percentage',
		container: '.container',
		expensesPercLabel: '.item__percentage',
		dateLabel: '.budget__title--month'
	};

	var formatNumber = function(num, type) {
			/*
			+ or - before number exactly 2 decimal points
			comma separating the thousands

			2310.4567 => + 2,310.46
			2000 -> + 2,000.00
			*/

			num = Math.abs(num);
			num = num.toFixed(2);
			numSplit = num.split('.');
			int = numSplit[0];
			if (int.length > 3) {
				int = int.substr(0, int.length - 3) + ',' + int.substr(int.length - 3, 3);
			}
			dec = numSplit[1];
			type === 'exp' ? sign = '-' : sign = '+';
			return type + ' ' + int + '.' + dec;
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
			newHtml = newHtml.replace('%value%', formatNumber(obj.value, type));

			// Insert the HTML into the DOM
			document.querySelector(element).insertAdjacentHTML('beforeend', newHtml);
		},

		deleteListItem: function(selectorID) {
			var el = document.getElementById(selectorID);
			el.parentNode.removeChild(el);
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
			var type;
			obj.budget > 0 ? type = 'inc' : type = 'exp';
			document.querySelector(DOMstrings.budgetLabel).textContent = formatNumber(obj.budget, type);
			document.querySelector(DOMstrings.incomeLabel).textContent = formatNumber(totoalInc, 'inc');
			document.querySelector(DOMstrings.expensesLabel).textContent = formatNumber(totalExp, 'exp');

			if（obj.percentage > 0）{
				document.querySelector(DOMstrings.percentageLabel).textContent = percentage + '%';
			} else {
			 document.querySelector(DOMstrings.percentageLabel).textContent = '---';
			}
		},

		displayPercentages: function(percentages) {
			var fields = document.querySelectorAll(DOMstrings.expensesPercLabel);
			var nodeListForEach = function(list, callback) {
				for (var i = 0; i < list.length; i++) {
					callback(list[i], i);
				}
			};

			nodeListForEach(fields, function(current, index) {
				if (percentages[index] > 0) {
					current.textContent = percentages[index] + "%";
				} else {
					current.textContent = '---';
				}
			});
		},

		displayMonth: function() {
			var now, months, month, year;
			now = new Date();
			// var christmas = new Date(2016, 11);

			months = ['January', 'February', 'March', 'April', 'May', 'June', 'July', 'Auguest', 'September', 'October', 'November', 'December'];
			month = new.getMonth();

			year = now.getFullYear();
			document.querySelector(DOMstrings.dateLabel).textContent = months[month - 1] + ' ' + year;			
		},



		getDOMstrings: function() {
			return DOMstrings;
		}
	};
})();

```


Step2: call UICtrl.displayMonth() in init() method.
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

		document.querySelector(DOM.container).addEventListener('click', ctrlDeleteItem);

	};

	var updateBudget = function() {
		// 1. Calculate the budget
		budgetCtrl.calculateBudget();
		// 2. Return the budget
		var budget = bubdgetctrl.getBudget();
		// 3. Display the budget on the UI
		console.log(budget);
	};

	var updatePercentages = function() {

		// 1. Calculate percentages
		// 2. Read percentages from the budget controller

		// 3. Update the UI with the new percentages


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

			// 6. Calculate and update percentage
			updatePercentages();
		}
	};

	var ctrlDeleteItem = function(event) {
		console.log(event.target);
		var itemID, splitID;
		itemID = event.target.parentNode.parentNode.parentNode.parentNode.id;
		if (itemID) {
			//inc-1
			splitID = itemID.split("-");
			type = splitID[0];
			ID = splitID[1];

			// 1. delete the item from the data structure
			budgetCtrl.deleteItem(type, ID);

			// 2. Delete the item from the UI
			UICtrl.deleteListItem(itemID);

			// 3. Update and show the new budget
			updateBudget();

			// 4. Calculate and update percentage
			updatePercentages();
		}


	};

	return {
		init: function() { //Our public init method
			console.log('Application has started.');
			UICtrl.displayMonth();
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


## 7. Finishing Touches: Improving the UX
- What you will learn in this lecture
	- How and when to use 'change' events.

Add 'change' event listener in setupEventListeners function in global app controller

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

		document.querySelector(DOM.container).addEventListener('click', ctrlDeleteItem);
		document.querySelector(DOM.inputType).addEventListener('change', UICtrl.changedType);
	};

	var updateBudget = function() {
		// 1. Calculate the budget
		budgetCtrl.calculateBudget();
		// 2. Return the budget
		var budget = bubdgetctrl.getBudget();
		// 3. Display the budget on the UI
		console.log(budget);
	};

	var updatePercentages = function() {

		// 1. Calculate percentages
		// 2. Read percentages from the budget controller

		// 3. Update the UI with the new percentages


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

			// 6. Calculate and update percentage
			updatePercentages();
		}
	};

	var ctrlDeleteItem = function(event) {
		console.log(event.target);
		var itemID, splitID;
		itemID = event.target.parentNode.parentNode.parentNode.parentNode.id;
		if (itemID) {
			//inc-1
			splitID = itemID.split("-");
			type = splitID[0];
			ID = splitID[1];

			// 1. delete the item from the data structure
			budgetCtrl.deleteItem(type, ID);

			// 2. Delete the item from the UI
			UICtrl.deleteListItem(itemID);

			// 3. Update and show the new budget
			updateBudget();

			// 4. Calculate and update percentage
			updatePercentages();
		}


	};

	return {
		init: function() { //Our public init method
			console.log('Application has started.');
			UICtrl.displayMonth();
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
		percentageLabel: '.budget__expenses--percentage',
		container: '.container',
		expensesPercLabel: '.item__percentage',
		dateLabel: '.budget__title--month'
	};

	var formatNumber = function(num, type) {
			/*
			+ or - before number exactly 2 decimal points
			comma separating the thousands

			2310.4567 => + 2,310.46
			2000 -> + 2,000.00
			*/

			num = Math.abs(num);
			num = num.toFixed(2);
			numSplit = num.split('.');
			int = numSplit[0];
			if (int.length > 3) {
				int = int.substr(0, int.length - 3) + ',' + int.substr(int.length - 3, 3);
			}
			dec = numSplit[1];
			type === 'exp' ? sign = '-' : sign = '+';
			return type + ' ' + int + '.' + dec;
		};

		var nodeListForEach = function(list, callback) {
			for (var i = 0; i < list.length; i++) {
				callback(list[i], i);
			}
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
			newHtml = newHtml.replace('%value%', formatNumber(obj.value, type));

			// Insert the HTML into the DOM
			document.querySelector(element).insertAdjacentHTML('beforeend', newHtml);
		},

		deleteListItem: function(selectorID) {
			var el = document.getElementById(selectorID);
			el.parentNode.removeChild(el);
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
			var type;
			obj.budget > 0 ? type = 'inc' : type = 'exp';
			document.querySelector(DOMstrings.budgetLabel).textContent = formatNumber(obj.budget, type);
			document.querySelector(DOMstrings.incomeLabel).textContent = formatNumber(totoalInc, 'inc');
			document.querySelector(DOMstrings.expensesLabel).textContent = formatNumber(totalExp, 'exp');

			if（obj.percentage > 0）{
				document.querySelector(DOMstrings.percentageLabel).textContent = percentage + '%';
			} else {
			 document.querySelector(DOMstrings.percentageLabel).textContent = '---';
			}
		},

		displayPercentages: function(percentages) {
			var fields = document.querySelectorAll(DOMstrings.expensesPercLabel);
			nodeListForEach(fields, function(current, index) {
				if (percentages[index] > 0) {
					current.textContent = percentages[index] + "%";
				} else {
					current.textContent = '---';
				}
			});
		},

		displayMonth: function() {
			var now, months, month, year;
			now = new Date();
			// var christmas = new Date(2016, 11);

			months = ['January', 'February', 'March', 'April', 'May', 'June', 'July', 'Auguest', 'September', 'October', 'November', 'December'];
			month = new.getMonth();

			year = now.getFullYear();
			document.querySelector(DOMstrings.dateLabel).textContent = months[month - 1] + ' ' + year;			
		},

		changedType: function() {
			var fields = document.querySelctorAll(
				DOMstrings.inputType + ',' +
				DOMstrings.inputDescription + ',' +
				DOMstrings.inputValue);

			nodeListForEach(fields, function(cur)) {
				cur.classList.toggle('red-focus');
			}),
			document.querySelector(DOMstrings.inputBtn).classList.toggle('red');
		},

		getDOMstrings: function() {
			return DOMstrings;
		}
	};
})();

```


## 8. Our Final Architecture
![Our Final Architecture](https://lh3.googleusercontent.com/1BZ8L7P6elWPyQ56s7jI0TBA3F5sUmuxL1_uIu3m0pXMlaDx-BcKV48byhiFRgSGy1rJZAAF0iGaxt7lF2Nsi-6Jzk20u1M7daIGZtgQdkQG5R_pJNUkCK2oKZiKc0dP8dXuMJktYnJTVhqn87Bz3LvhpEHUiCKxrS2t320cgh8AfXZp62zqNOBECAENb05E0DdWAbhfAL7fJWr6dv-GZnnNuAfWo2NpnB1QgkENFaCkYunA-PUlVpSfxHeIimwRxlaQ7WOeYfdEGB5tYHXoEHCS3Pt3YNzpEHeE9jNcsxw4lODEoV7Qy05svlQg1I35scb5TQ4uzjtU5Qly4nAN3dAJVLlONsqwzwWEwq-E-qr7A12p83Mk-BmIL_geuwPm1M831aFe3J-fIxsmLqXYxk44P-CXVg9G2fEBmHChZ2gRfKqTCcBWhTYAgXA5rldeIr7tZUQNW22eSgTXrgsO64CWs6KIkh8Yjfww2DeDefSkWj7rhRzXj9iVN9WxcaDkjR2jlM-AHA3jdCfsQxajjsv5wonKESZz4s_1OMq6cHcxGbRtnxAMraOTeme20vokZLjvp4A3hsmmuXOjqaK5Nvj9QlWap457OMrNZLvGilJB2mozA-sSy15m7JWYeG0gQGKjtCP5TEt68pOWVo9_GEc20YeAkopayGh5WGK21Q=w1274-h709-no)
