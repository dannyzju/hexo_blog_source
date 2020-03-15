---
title: 'Put It All Together: The Budget App Project: Part II'
date: 2017-05-29 15:36:44
tags:
- 学习笔记
- tech
- JavaScript
---

## 1. Project Planning and Architecture: Step 2
### 1.1. What We Just Completed
![What We Just Completed](https://lh3.googleusercontent.com/lWHSuBs8felsWHAkvqpV00aL1I16pvwOuyWJWBIGCKWBdNmKtZLINWu4kMviBUSfR8sqIWtXkYQXV89q6G3uuDFVZOEb1qHgoiP_XFbobM0MTD7QuKl2XYARjHQ2SMdNzOjTLOxHUQLFAsdFbOz1ZQjWx52FKDHblkfwA6nu9dIOSRoRm4e_KIsybUsWC2_3HWlL40M96YR6PFYoqbp7AGyr5jEvPBaByzglQtjN3Nqq5bQxSRqjSoZdt5LvRvpGSf5qiJ8CUlmWTN3bIASzu7QTNWuk2nPKAgKRSeI6lk1iP5s6SM3Q0-lDVfxUf9oYJLxtmQwKz2WDG9ZaF8dbJ5fOxUNArNaWEKH0UWGOkWIKCn0X0_S2nd-RBdRTBb5k0dsUTx9DifrNOjMTu-jj5gfKha6vUrkh0Sr-3-x_J2i8ZctWlOdf89DEMdmeZuaOoU4YefaFka0r5UoFiyxCl6YDn26JEOccMDPCsK_4laOExPeIle56252nE1AmdnpQkzGew95GnUPYsJBPYql4QQfMhHG3Jjs8i2FFJEeja56_8-q_Mj_9NBR5OjbLhExeCmzq7HXPKh0yY37j-WTbJkJRU_sL31w5AI9kv15FvyHFtUL8a5HN-Kv6uqnlCiQpsXOycBoH_0iMtKMm91v87Sa38PJ8duw7KubvV-cFTw=w1734-h1010-no)

### 1.2. Panning: Step 2
![Panning: Step 2](https://lh3.googleusercontent.com/GE0EEABtsEXmgyU9mkcrKRA_8HCx9Ce0Aql32TGBRA3kvp3lK93plD9jxezzD1oQBfJnch59NZfYCBH4VJE41u1_p-496CSU-ilLb6sl9xcAaeLRUKyya8PL6aEdRguUj1yaJYltix4dFNtLzmz5kfsNdfDolbVj0TDq05U2GYQEyFWlC2DHILnWQ2C6gxCT5rOZ50E7d8pzEmLILfBD4VukS2Tju3Obail2Csd2mRV4ty6eFk7FtfVBj2Wqd2arQ7b36FICt_PKKwXiybATO1SF_ilm30l12ge58n5PVittFmI0fMBAVglKi7gNBwqTVqc8qMtIRr8jopHCDyBS6_zkw_NCoGzGAol8eQvR_MJirBeBhQEUI66mXDDUk-qmODARUteDvKSQgLdBDA0J2MwrMh_iEBYB8kcHMhAjVGtsXJo-WkGeiCaEwQ_MMLJAL2bvnqxrkgJ-39H84SDVMlfA_s1t7npm_AaIUmyWBWr7PtgaCzNSW_wiCOBoA4Ux5YPufYK36soW7GvTfvr2saHqFb4nv0-GT5vILIXNkyLgW7RDOMwjiYFaym79MJiWREGM6EaHQeWm4LVHwUJ9ezfM1DUHn9tBnE0ECT6oSWyQgCXOARZhkV-SJpZIsTPuecQtuV_km9g9DBdXCWgV793Nr5ABh-B1e9sqW1bo-g=w1734-h850-no)

## 2. Event Delegation

### 2.1. Event Bubbling, Target Element and Event Delegation
![Event Bubbling, Target Element and Event Delegation](https://lh3.googleusercontent.com/--HVptQAUvm5pPbpqe3db6umeD2fiDOmNqVPk9IN40Hveu52sLVpUN7syCmeZChKc7-vv-rlcc7O3u-8Qu58L-psHxAPryPywwTaN1eSxTYUz8YCou1xrhIpcRG2udvNmp4jxuOT2pieJH68523eCjGOu8rG0M99FQu_PZqbte2PIGStrJxRyWoKr9GO5zaWzzHmbp_NvjJrRBF8c_tiiSIdhY_1ACeDu5vwJMmI7AwsahDiDJ2JYdYOZK0DdiJd3vMYJxWqQILsldxGmDllXiYT98peKz8LNKgyqKZqnp7HQtWU4qbnEw2y0kv6jsPyf71Hd44rsY1f2Mwlm2TSl9q7DGEVDlzlZ0oo82EhCNmF1Wr_RKdbMkgO-pMKh5iQp4OjPYdzY56YPblCOaw47JnOKXvCr36_RYiF-90HkEuT1tdrSF3nYIkFyaKIxfMxb9V1NXKocKdfz48aBiHW7UMVus-3fp4td61oyW66B3uG4QpJOg8fVpNvj59-CokV52UhcwGtajTwqpWdHNB5u7942I7mb0HwwxY7q4w1Z1snahSkZ_FuvamtjQ1MEmocxQPHFd4NrL71oMigqd2AqSy2mb3VW0Xq7LmhtshbrQrqhlWeG0ubgl4yYN4u8Hej2gOTvRNiUKGGbWMNXvUZHyx--imq2m5ydn2IzYHbNw=w819-h362-no)

**`Event bubbling`** mean that when an event is fired or triggered on some DOM element, for example,by clicking on our button here on the right side, then the exact same event is also triggered on all of the parent elements.


**`Event delegation`** refers to the process of using event propagation (bubbling) to handle events at a higher level in the DOM than the element on which the event originated. It allows us to attach a single event listener for elements that exist now or in the future.

### 2.2. Use Cases for Event Delegation
1. When we have an element with lots of child elements that we are interested in;

2. When we want an event handler attached to an element that is not yet in the DOM when our page is loaded.

## 3. Setting up the Delete Event Listener Using Event Delegation

- **`What you will learn in this section:`**
	- How to use event delegation in practice;
	- How to use IDs in HTML to connect the UI with the data model;
	- How to use the parentNode property for DOM traversing.

- Action Items
	- Add container in UI Controller DOMstrings;
	- Update setupEventListners in app controller;
	- Create ctrlDeleteItem method for event listener.

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
		container: '.container'
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

			// 2. Delete the item from the UI

			// 3. Update and show the new budget
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



## 4. Deleting an Item from our Budget Controller

- **`What you will learn in this section:`**
	- Yet another method to loop over an array: map;
	- How to remove elements from an array using the splice method.


Add deleteItem Method in Budget Controller

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


Call deleteItem method in App Controller ctrlDeleteItem:
```javaScript

	var ctrlDeleteItem = function(event) {
		console.log(event.target);
		var itemID, splitID;
		itemID = event.target.parentNode.parentNode.parentNode.parentNode.id;
		if (itemID) {
			//inc-1
			splitID = itemID.split("-");
			type = splitID[0];
			ID = parseInt(splitID[1]);

			// 1. delete the item from the data structure
			budgetCtrl.deleteItem(type, ID);

			// 2. Delete the item from the UI

			// 3. Update and show the new budget
		}
	};

```

## 5. Deleting an Item from the UI

- **`What you will learn in this section:`**
	- More DOM manipulation: how to remove an element from the DOM.

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
		container: '.container'
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

		getDOMstrings: function() {
			return DOMstrings;
		}
	};
})();

```


Call UICtrl.deleteListItem and updateBudget methods in App Controller ctrlDeleteItem:
```javaScript

	var ctrlDeleteItem = function(event) {
		console.log(event.target);
		var itemID, splitID;
		itemID = event.target.parentNode.parentNode.parentNode.parentNode.id;
		if (itemID) {
			//inc-1
			splitID = itemID.split("-");
			type = splitID[0];
			ID = parseInt(splitID[1]);

			// 1. delete the item from the data structure
			budgetCtrl.deleteItem(type, ID);

			// 2. Delete the item from the UI
			UICtrl.deleteListItem(itemID);

			// 3. Update and show the new budget
			updateBudget();
		}
	};
```
