<script lang="ts">
  import { onMount } from 'svelte';

  const palavras = ["AVIÃO", "CARRO", "TREM", "REELS"];
  const tamanho = 10;

  let grade: string[][] = [];
  let selecao: [number, number][] = [];
  let palavrasEncontradas: string[] = [];

  function gerarGrade() {
    grade = Array.from({ length: tamanho }, () =>
      Array.from({ length: tamanho }, () =>
        String.fromCharCode(65 + Math.floor(Math.random() * 26))
      )
    );

    palavras.forEach(palavra => {
      const linha = Math.floor(Math.random() * tamanho);
      const inicio = Math.floor(Math.random() * (tamanho - palavra.length));
      for (let i = 0; i < palavra.length; i++) {
        grade[linha][inicio + i] = palavra[i];
      }
    });
  }

  function selecionarLetra(i: number, j: number) {
    const index = selecao.findIndex(([x, y]) => x === i && y === j);
    if (index > -1) {
      selecao.splice(index, 1);
    } else {
      selecao.push([i, j]);
    }
  }

  function verificarSelecao() {
    const letras = selecao.map(([x, y]) => grade[x][y]).join("");
    if (palavras.includes(letras)) {
      if (!palavrasEncontradas.includes(letras)) {
        palavrasEncontradas.push(letras);
      }
      alert(`Você encontrou: ${letras}`);
    } else {
      alert("Palavra incorreta");
    }
    selecao = [];
  }

  onMount(() => {
    gerarGrade();
  });
</script>

<style>
  table.caca-palavras {
    margin: auto;
    border-collapse: collapse;
    background-color: yellow;
  }

  table.caca-palavras td {
    border: 1px solid black;
    width: 32px;
    height: 32px;
    text-align: center;
    font-weight: bold;
    cursor: pointer;
    color: black;
  }

  table.caca-palavras td.selected {
    background-color: green;
    color: white;
  }

  ul {
    list-style: none;
    padding: 0;
    text-align: center;
    margin: 0 auto;
  }

  ul li {
    display: inline-block;
    margin: 0 12px;
  }

  button {
    padding: 6px 12px;
    margin: 4px;
    font-weight: bold;
    cursor: pointer;
    transition: all 0.1s ease;
    border: 2px solid #444;
    background-color: #eee;
    user-select: none;
    white-space: nowrap;
  }

  button:active {
    transform: translateY(2px);
    box-shadow: none;
  }

  button.found {
    background-color: #4caf50;
    color: white;
    border-color: #3e8e41;
    box-shadow: inset 2px 2px 5px rgba(0,0,0,0.3);
    cursor: default;
    transform: translateY(2px);
  }
</style>

<h2>Jogo de Caça-Palavras</h2>

<table class="caca-palavras">
  {#each grade as linha, i}
    <tr>
      {#each linha as letra, j}
        <td
          on:click={() => selecionarLetra(i, j)}
          class:selected={selecao.some(([x, y]) => x === i && y === j)}
        >
          {letra}
        </td>
      {/each}
    </tr>
  {/each}
</table>

<br />

<h4>Palavras para encontrar:</h4>
<ul>
  {#each palavras as palavra}
    <li>
      <button
        class:found={palavrasEncontradas.includes(palavra)}
        disabled={palavrasEncontradas.includes(palavra)}
      >
      
        {palavra}
      </button>
    </li>
  {/each}
</ul>


<button on:click={verificarSelecao}>Verificar Palavra</button>

