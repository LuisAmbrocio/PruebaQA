Se agrega codigo corregido del dia 23/05/2023, ya que repositorio no carga las correciones de visual studio.

<!DOCTYPE html>
<html lang="en-us">
  <head>
    <meta charset="utf-8">

    <title>Juego de adivina tu número</title>

    <style>
      html {
        font-family: sans-serif;
      }
      body {
        width: 50%;
        max-width: 800px;
        min-width: 480px;
        margin: 0 auto;
      }

	.form input[type="number"] {
        width: 200px;
      }
      .lastResult {
        color: white;
        padding: 3px;
      }
    </style>
  </head>

  <body>
      <h1>Juego Adivina tu número</h1>

      <p>Hemos seleccionado un número aleatorío entre 1 a 100. Trata de adivinar el número, en un total de 10 turnos o menos. No te preocupes, te diremos sí el número es más alto o más bajo </p>

<div class="form">
  <label for="guessField">Ingresa el número a adivinar: </label><input type="number" min="1" max="100" required id="guessField" class="guessField">
  <input type="submit" value="Ingresar el número aleatorio" class="guessSubmit">
</div>

<div class="resultParas">
  <p class="guesses"></p>
  <p class="lastResult"></p>
  <p class="lowOrHi"></p>
</div>

</body>

<script>
  let randomNumber = Math.floor(Math.random() * 100) + 1;

  const guesses = document.querySelector('.guesses');
  const lastResult = document.querySelector('.lastResult');
  const lowOrHi = document.querySelector('.lowOrHi');
  const guessSubmit = document.querySelector('.guessSubmit');
  const guessField = document.querySelector('.guessField');

  let guessCount = 1;
  let resetButton;

  function checkGuess() {

    const userGuess = Number(guessField.value);
    if(guessCount === 1) {
      guesses.textContent = 'Número aleatorio anterior: ';
    }
    guesses.textContent += userGuess + ' ';

    if(userGuess === randomNumber) {
      lastResult.textContent = 'Felicitaciones! adivinaste el número!';
      lastResult.style.backgroundColor = 'green';
      lowOrHi.textContent = '';
      setGameOver();
    } else if(guessCount === 10) {
      lastResult.textContent = '!!!Pérdistes!!!';
      lowOrHi.textContent = '';
      setGameOver();
    } else {
      lastResult.textContent = 'Incorrecto! ';
      lastResult.style.backgroundColor = 'red';
      if(userGuess < randomNumber) {
        lowOrHi.textContent = 'El número es mayor!';
      } else if(userGuess > randomNumber) {
        lowOrHi.textContent = 'El número es menor!';
      }
    }

    guessCount++;
    guessField.value = '';
    guessField.focus();
  }
  guessSubmit.addEventListener('click', checkGuess);

  function setGameOver() {
	  guessField.disabled = true;
	  guessSubmit.disabled = true;
	  resetButton = document.createElement('button');
	  resetButton.textContent = 'Comienza un nuevo juego';
	  document.body.appendChild(resetButton);
	  resetButton.addEventListener('click', resetGame);
  }

  function resetGame() {
	  guessCount = 1;

	  const resetParas = document.querySelectorAll('.resultParas p');
	  for(const resetPara of resetParas) {
		  resetPara.textContent = '';
	  }

	  resetButton.parentNode.removeChild(resetButton);
	  guessField.disabled = false;
	  guessSubmit.disabled = false;
	  guessField.value = '';
	  guessField.focus();

	  lastResult.style.backgroundColor = 'white';

	  randomNumber = Math.floor(Math.random()*100) + 1;
  }
</script>
</html>
