<h1 class="glass">Enchanted Hunt</h1>
<hr />

<br />
<div class="container">
  <table class="glass">
    <tbody>
      <tr>
        <td>
          <a href="/jogo"><button>Start the Game</button></a>
          <br /><br />
          <a href="/sobre"><button>About</button></a>
          <br /><br />
          <a href="/ajuda"><button>Help</button></a>
          <br /><br />
          <a href="/ranking"><button>Ranking</button></a>
          <br /><br />
        </td>
      </tr>
    </tbody>
  </table>

  <table class="glass">
    <tbody>
      <tr>
        <td style="text-align: right;">
          <img src="/manu.png" height="350" width="auto" />
        </td>
      </tr>
    </tbody>
  </table>
</div>

<hr />

<style>
  .glass {
    background: rgba(255, 255, 255, 0.15);
    border-radius: 10px;
    padding: 20px;
    backdrop-filter: blur(10px);
    -webkit-backdrop-filter: blur(10px);
    box-shadow: 0 8px 32px 0 rgba(31, 38, 135, 0.37);
    color: white;
  }

  .container {
    display: flex;
    justify-content: space-around;
    align-items: center;
    flex-wrap: wrap;
    margin: 50px;
  }

  button {
    padding: 10px 20px;
    font-size: 1.1rem;
    background-color: rgba(0, 0, 0, 0.5);
    border: none;
    border-radius: 8px;
    color: white;
    cursor: pointer;
  }

  button:hover {
    background-color: rgba(0, 0, 0, 0.7);
  }

  h1 {
    text-align: center;
    font-size: 3rem;
    margin-top: 40px;
    color: white;
  }

  hr {
    border: none;
    border-top: 1px solid white;
    width: 80%;
    margin: 20px auto;
  }

  body {
    background: linear-gradient(to right, #0f2027, #203a43, #2c5364);
    font-family: sans-serif;
  }
</style>

