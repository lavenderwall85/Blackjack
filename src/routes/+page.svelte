<script>
    // Mazo de cartas 
    let mazo = [
      { emoji: '🍎', valor: 1 }, { emoji: '🍌', valor: 2 }, { emoji: '🍒', valor: 3 },
      { emoji: '🍇', valor: 4 }, { emoji: '🍉', valor: 5 }, { emoji: '🍍', valor: 6 },
      { emoji: '🥭', valor: 7 }, { emoji: '🍋', valor: 8 }, { emoji: '🍊', valor: 9 },
      { emoji: '🍓', valor: 10 }
    ];
  
    let misCartas = []; 
    let miPuntaje = 0; 
  
    function sacarCarta() {
      // carta aleatoria
      let indice = Math.floor(Math.random() * mazo.length);
      let carta = mazo[indice];
  
      // Agregar la carta y sumar su valor al puntaje
      misCartas = [...misCartas, carta];
      miPuntaje += carta.valor;
    }
    function reiniciarJuego() {
      misCartas = [];
      miPuntaje = 0;
    }
  </script>
  
  <style>
    .juego {
      position: absolute;
      max-width: 520px;
      width: 100%;
      height: 310px;
      background: #F5F5F5;
      padding: 15px 0;
      box-shadow: 4px 1px 9px 0px rgba(0,0,0,0.63);
      top: 50%;
      left: 50%;
      transform: translate(-50%, -50%);
      border-radius: 10px;
      text-align: center;
      font-family: Arial, sans-serif;
    }
    .cartas {
      display: flex;
      justify-content: center;
      gap: 10px;
      font-size: 2.5rem;
    }
    .boton {
      padding: 10px;
      margin-top: 20px;
      background-color: #4CAF50;
      color: white;
      border: none;
      border-radius: 5px;
      cursor: pointer;
    }
    .boton:disabled {
      background-color: gray;
      cursor: not-allowed;
    }

    .boton-reiniciar:disabled{
      background-color: gray;
      cursor: not-allowed;
    }

    .boton-reiniciar {
      padding: 10px;
      margin-top: 20px;
      background-color: #f44336;
      color: white;
      border: none;
      border-radius: 5px;
      cursor: pointer;
    }
  </style>
  
  <div class="juego">
    <h1>Blackjack con Emojis</h1>
    <p>Tus cartas:</p>
    <div class="cartas">
      {#each misCartas as carta}
        <span>{carta.emoji}</span>
      {/each}
    </div>
    <p>Puntaje: {miPuntaje}</p>
    <button class="boton" on:click={sacarCarta} disabled={miPuntaje >= 21}>
      Sacar Carta
    </button>
    <button class="boton-reiniciar" on:click={reiniciarJuego} disabled={miPuntaje <= 0}>
      Reiniciar
    </button>
  {#if miPuntaje > 21}
    <p>¡Perdiste! Te pasaste de 21.</p>
  {:else if miPuntaje == 21}
    <p>¡Felicidades! ¡Ganaste con un 21 perfecto!</p>
  {/if}
  </div>
  