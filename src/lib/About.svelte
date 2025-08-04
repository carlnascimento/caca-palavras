<style>
  .about-container {
    padding: 20px;
    color: white;
  }

  .about-header {
    display: flex;
    justify-content: space-between;
    align-items: center;
    background: rgba(255, 255, 255, 0.1);
    backdrop-filter: blur(10px);
    -webkit-backdrop-filter: blur(10px);
    border-radius: 15px;
    padding: 20px;
    margin-bottom: 20px;
  }

  
/* Opcional: estilo glass também no título */
h1.glass {
  display: inline-block;
  padding: 20px 40px;
  background: rgba(255, 255, 255, 0.1);
  backdrop-filter: blur(8px);
  border-radius: 20px;
  box-shadow: 0 4px 30px rgba(0, 0, 0, 0.2);

/* Sombra para melhorar a legibilidade */
  text-shadow:
    2px 2px 3px black,
    -2px -2px 3px black,
    2px -2px 3px black,
    -2px 2px 3px black;
}

  .logo-if {
    height: 60px;
    border-radius: 10px;
    background: rgba(255, 255, 255, 0.2);
    backdrop-filter: blur(8px);
    -webkit-backdrop-filter: blur(8px);
    padding: 5px;
  }

  .subtitulo {
    margin-bottom: 15px;
    font-size: 1.2em;
    padding: 10px;
    background: rgba(255, 255, 255, 0.1);
    backdrop-filter: blur(8px);
    -webkit-backdrop-filter: blur(8px);
    border-radius: 10px;
  }

  .tabelas-wrapper {
    display: flex;
    flex-wrap: wrap;
    gap: 20px;
    justify-content: center;
  }

  .participantes-tabela {
    background: rgba(255, 255, 255, 0.12);
    backdrop-filter: blur(12px);
    -webkit-backdrop-filter: blur(12px);
    border-radius: 15px;
    padding: 15px;
    color: black;
    font-weight: bold;
  }

  .participantes-tabela td {
    padding: 10px;
    vertical-align: middle;
  }

  .participantes-tabela img {
    width: 80px;
    height: 80px;
    object-fit: cover;
    border-radius: 50%;
    border: 2px solid #ffffff44;
    background: rgba(255, 255, 255, 0.2);
    backdrop-filter: blur(6px);
    -webkit-backdrop-filter: blur(6px);
  }
</style>

<script lang="ts">
  // Sem nada específico aqui
</script>

<div class="about-container">
  <div class="about-header">
    <h1>Sobre os Participantes</h1>
    <img src="/if.png" alt="Logo IF" class="logo-if" />
  </div>

  <h4 class="subtitulo">Este jogo foi desenvolvido por:</h4>

  <div class="tabelas-wrapper">
    <table class="participantes-tabela">
      <tbody>
        <tr>
          <td><img src="/carlos.jpg" alt="Carlos" /></td>
          <td>Carlos José do Nascimento Cruz</td>
        </tr>
        <tr>
          <td><img src="/manuela.jpeg" alt="Manuela" /></td>
          <td>Manuela Maria do Nascimento</td>
        </tr>
        <tr>
          <td><img src="/reynaldo.jpeg" alt="Reynaldo" /></td>
          <td>Reynaldo Souza Ramos Júnior</td>
        </tr>
      </tbody>
    </table>

    <table class="participantes-tabela">
      <tbody>
        <tr>
          <td><img src="/jackson.jpeg" alt="Jackson" /></td>
          <td>Jackson Tomaz de Albertim</td>
        </tr>
        <tr>
          <td><img src="/luiz.jpeg" alt="Luiz" /></td>
          <td>Luiz Cláudio Silva da Cunha</td>
        </tr>
        <tr>
          <td><img src="/kaua.jpeg" alt="Kauã" /></td>
          <td>Cauã Salustiano</td>
        </tr>
      </tbody>
    </table>
  </div>
</div>

