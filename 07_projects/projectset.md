# Projects related to DOM

## project link
https://stackblitz.com/edit/dom-project-chaiaurcode?file=1-colorChanger%2Fchaiaurcode.js

# solution code 

## project 1

```JAVASCRIPT 
const buttons = document.querySelectorAll('.button');
const body = document.querySelector("body");

buttons.forEach(function(button) {
  console.log(button);
  button.addEventListener('click',function(e){
    console.log(e)
    console.log(e.target)
    if(e.target.id === 'grey' ){
      body.style.backgroundColor = e.target.id;
    }
    if(e.target.id === 'white' ){
      body.style.backgroundColor = e.target.id;
    }
    if(e.target.id === 'blue' ){
      body.style.backgroundColor = e.target.id;
    }
    if(e.target.id === 'yellow' ){
      body.style.backgroundColor = e.target.id;
    }
  })
});

```

## project 2 

```JAVASCRIPT
const form = document.querySelector('form')

form.addEventListener('submit',function(e){
  e.preventDefault()

  const height = parseInt(document.querySelector('#height').value)

  const weight = parseInt(document.querySelector('#weight').value)

  const results = document.querySelector('#results')

  if (height === '' || height < 0 || isNaN(height)) {
    results.innerHTML = 'Please give a valid height';
  }
  else  if (weight === '' || weight < 0 || isNaN(weight)) {
    results.innerHTML = 'Please give a valid weight';
  }
  else{
    const bmi = (weight / ((height*height)/10000)).toFixed(2)
    //show the result
    // results.innerHTML = `<span>${bmi}</span>`

    if(bmi<18.6){
      results.innerHTML = `Under weight <br>BMI : ${bmi}`
    }
    if(18.6<bmi<24.9){
       results.innerHTML = `Normal Range <br>BMI : ${bmi}`
    }
    if (bmi>24.9){
       results.innerHTML = `Over Weight <br>BMI : ${bmi}`
    }
  }
});

```

## project 3

```JAVASCRIPT
const clock = document.getElementById('clock')
//const clock = document.querySelector('#clock')

setInterval(function(){
  let date = new Date();
  // console.log(date.toLocaleTimeString());
  clock.innerHTML = date.toLocaleTimeString();
}, 1000)

```
## project 4
```JAVASCRIPT

let randomNumber = parseInt(Math.random() * 100 + 1);

const submit = document.querySelector('#subt');
const userInput = document.querySelector('#guessField');
const guessSlot = document.querySelector('.guesses');
const remaining = document.querySelector('.lastResult');
const lowOrHi = document.querySelector('.lowOrHi');
const startOver = document.querySelector('.resultParas');

const p = document.createElement('p');

let prevGuess = [];
let numGuess = 1;

let playGame = true;

if (playGame) {
  submit.addEventListener('click', function (e) {
    e.preventDefault();
    const guess = parseInt(userInput.value);
    console.log(guess);
    validateGuess(guess);
  });
}

function validateGuess(guess) {
  if (isNaN(guess)) {
    alert('PLease enter a valid number');
  } else if (guess < 1) {
    alert('PLease enter a number more than 1');
  } else if (guess > 100) {
    alert('PLease enter a  number less than 100');
  } else {
    prevGuess.push(guess);
    if (numGuess === 11) {
      displayGuess(guess);
      displayMessage(`Game Over. Random number was ${randomNumber}`);
      endGame();
    } else {
      displayGuess(guess);
      checkGuess(guess);
    }
  }
}

function checkGuess(guess) {
  if (guess === randomNumber) {
    displayMessage(`You guessed it right`);
    endGame();
  } else if (guess < randomNumber) {
    displayMessage(`Number is TOOO low`);
  } else if (guess > randomNumber) {
    displayMessage(`Number is TOOO High`);
  }
}

function displayGuess(guess) {
  userInput.value = '';
  guessSlot.innerHTML += `${guess}, `;
  numGuess++;
  remaining.innerHTML = `${11 - numGuess} `;
}

function displayMessage(message) {
  lowOrHi.innerHTML = `<h2>${message}</h2>`;
}

function endGame() {
  userInput.value = '';
  userInput.setAttribute('disabled', '');
  p.classList.add('button');
  p.innerHTML = `<h2 id="newGame">Start new Game</h2>`;
  startOver.appendChild(p);
  playGame = false;
  newGame();
}

function newGame() {
  const newGameButton = document.querySelector('#newGame');
  newGameButton.addEventListener('click', function (e) {
    randomNumber = parseInt(Math.random() * 100 + 1);
    prevGuess = [];
    numGuess = 1;
    guessSlot.innerHTML = '';
    remaining.innerHTML = `${11 - numGuess} `;
    userInput.removeAttribute('disabled');
    startOver.removeChild(p);

    playGame = true;
  });
}


```