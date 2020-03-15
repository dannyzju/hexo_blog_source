---
title: 'JavaScript in the Browser: DOM Manipulation and Events'
date: 2017-04-05 06:44:25
tags:
- 学习笔记
- tech
- JavaScript
---

## 1. The DOM and DOM Manipulation
- DOM: Document Object Model;
- Structured representation of an HTML document;
- The DOM is used to connect webpages to scripts like JavaScript;
- For each HTML box, there is an object in the DOM that we can access and interact with.

![DOM](https://lh3.googleusercontent.com/opF1GsIL8wI2VAPukMjRs_qVBbUa2SFB7IcszMYq4Y4Rhm31n4gtbs1dJZAwrziMJS4-wQn4OxbYBzN3_jLw8J7Fi4XG43rFJSnO6s1ODZG9r1vRMGqLybAWUzggx4lbGhzPJy_NZ6iwhv29W8Ko0mk-im0KsEg0ChQOH9Haxup8w-jkv2mRGqUQy01uUcWsEWU1SjMge3SqI3giiUh-0j9l2OVf8BDW6rKY6yvWyqeTdOYHnVma0D9MCuFcmJCInlpOAtaTXiiRkRJNuZAoVeOvSN0GsblKPvxS_lsoiJiA4WEnq-Y73Ud2OtGlC-_m0iE67Atr1i5Skm1x0kIVy-jpGxPFj0RKiVGlha2saK9izFfFK5-a0KSg_W0DxfjESVcSboe4xZO5JMeHdb6RnZIugIFRi2Q_UHxQtuqw5s3R7LXXRdQktEidCrIz3QnFGMm4D07Lx6fO6jKflunl30_do5_0aaOaitVKy_AV5EEc-luK8X5EAPyB8PzuWQaT_6rfdK7TbuRuob3JmrFzvBmxglZjxb6tY-LACSogxScpISC5MoYyUEP9HIzOkt-LprxJ0R19VN01FEyTrkpEU7TbX0D0qQwEDDGxb8tSnTBpdzUwzDfHUNMJijQjxlnfQ1HL8knMIyhz0ZPQoAmcrpARr1W9N9N5UkVMpv_kMQ=w1192-h1019-no)

## 2. DOM Access and Manipulation
To get a random number from 1 to 6:
```javaScript
	var dice = Math.floor(Math.random() * 6) + 1;
```

Select an element using query selector:
```javaScript
document.querySelector('#current-' + activePlayer).textContent;
document.querySelector('#current-' + activePlayer).innerHTML;
document.querySelector('.dice').style.display;
```

Select an element using getElementById: (faster!)
```javaScript
document.getElementById('score-0').textContent = '0';
```

## 3. Events and Event Handling
- **Events**: Notifications that are sent to notify the code that something happened on the webpage;
- Examples: clicking a button, resizing a window, scrolling down or pressing a key;
- **Event listener**: A function that performs an action based on a certain event. It waits for a specific event to happen.

Add an event listener for an element:
```javaScript
document.querySelector('.btn-roll').addEventListener('click', function() { //An anonymous function, which does not have a name, and can not be used elsewhere.
	//Do something.
});

```

## 4. DRY(Don’t Repeat Yourself) Principle
For the same code used in different places, wrap it up with a function, like the init() and nextPlayer() in the project.

## 5. State Variables
In this example, use `gamePlaying` as a state variable to stop the game after a win.

## 6. Complete JavaScript Code
```javaScript
/*
GAME RULES:

- The game has 2 players, playing in rounds
- In each turn, a player rolls a dice as many times as he whishes. Each result get added to his ROUND score
- BUT, if the player rolls a 1, all his ROUND score gets lost. After that, it's the next player's turn
- The player can choose to 'Hold', which means that his ROUND score gets added to his GLBAL score. After that, it's the next player's turn
- The first player to reach 100 points on GLOBAL score wins the game

*/

var scores, roundScore, activePlayer, gamePlaying;

init();


document.querySelector('.btn-roll').addEventListener('click', function() {
    if(gamePlaying) {
        // 1. Random number
        var dice = Math.floor(Math.random() * 6) + 1;

        //2. Display the result
        var diceDOM = document.querySelector('.dice');
        diceDOM.style.display = 'block';
        diceDOM.src = 'dice-' + dice + '.png';


        //3. Update the round score IF the rolled number was NOT a 1
        if (dice !== 1) {
            //Add score
            roundScore += dice;
            document.querySelector('#current-' + activePlayer).textContent = roundScore;
        } else {
            //Next player
            nextPlayer();
        }
    }    
});


document.querySelector('.btn-hold').addEventListener('click', function() {
    if (gamePlaying) {
        // Add CURRENT score to GLOBAL score
        scores[activePlayer] += roundScore;

        // Update the UI
        document.querySelector('#score-' + activePlayer).textContent = scores[activePlayer];

        // Check if player won the game
        if (scores[activePlayer] >= 100) {
            document.querySelector('#name-' + activePlayer).textContent = 'Winner!';
            document.querySelector('.dice').style.display = 'none';
            document.querySelector('.player-' + activePlayer + '-panel').classList.add('winner');
            document.querySelector('.player-' + activePlayer + '-panel').classList.remove('active');
            gamePlaying = false;
        } else {
            //Next player
            nextPlayer();
        }
    }
});


function nextPlayer() {
    //Next player
    activePlayer === 0 ? activePlayer = 1 : activePlayer = 0;
    roundScore = 0;

    document.getElementById('current-0').textContent = '0';
    document.getElementById('current-1').textContent = '0';

    document.querySelector('.player-0-panel').classList.toggle('active');
    document.querySelector('.player-1-panel').classList.toggle('active');

    //document.querySelector('.player-0-panel').classList.remove('active');
    //document.querySelector('.player-1-panel').classList.add('active');

    document.querySelector('.dice').style.display = 'none';
}

document.querySelector('.btn-new').addEventListener('click', init);

function init() {
    scores = [0, 0];
    activePlayer = 0;
    roundScore = 0;
    gamePlaying = true;

    document.querySelector('.dice').style.display = 'none';

    document.getElementById('score-0').textContent = '0';
    document.getElementById('score-1').textContent = '0';
    document.getElementById('current-0').textContent = '0';
    document.getElementById('current-1').textContent = '0';
    document.getElementById('name-0').textContent = 'Player 1';
    document.getElementById('name-1').textContent = 'Player 2';
    document.querySelector('.player-0-panel').classList.remove('winner');
    document.querySelector('.player-1-panel').classList.remove('winner');
    document.querySelector('.player-0-panel').classList.remove('active');
    document.querySelector('.player-1-panel').classList.remove('active');
    document.querySelector('.player-0-panel').classList.add('active');
}

//document.querySelector('#current-' + activePlayer).textContent = dice;
//document.querySelector('#current-' + activePlayer).innerHTML = '<em>' + dice + '</em>';
//var x = document.querySelector('#score-0').textContent;

```

## 7. Project Demo
[Demo](http://dannyzhang.run/projects/pigGame)
