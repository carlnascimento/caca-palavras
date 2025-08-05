<script lang="ts">
    import { onMount } from 'svelte';

    const textos = [
        "A energia solar é uma das fontes de energia limpa mais promissoras para o futuro.",
        "A energia eólica transforma o vento em eletricidade sem emitir gases poluentes.",
        "A energia hidráulica aproveita a força da água para gerar energia renovável.",
        "A biomassa é uma alternativa ecológica para geração de energia.",
        "A energia geotérmica utiliza o calor interno da Terra como fonte energética.",
        "Painéis solares fotovoltaicos convertem luz do sol diretamente em eletricidade.",
        "A energia das marés pode ser aproveitada como fonte limpa e previsível.",
        "Carros elétricos ajudam a reduzir a emissão de carbono no transporte urbano.",
        "A eficiência energética contribui para o uso consciente da eletricidade.",
        "Fontes renováveis são essenciais para mitigar as mudanças climáticas.",
        "O uso de energia limpa melhora a qualidade do ar nas cidades.",
        "Tecnologias verdes promovem a sustentabilidade ambiental.",
        "O sol é uma fonte inesgotável de energia renovável.",
        "A redução de carbono é fundamental para frear o aquecimento global.",
        "Investimentos em energia limpa crescem em todo o mundo."
    ];

    let indiceAtual = 0;
    let texto: string = textos[indiceAtual];

    let palavrasParaEncontrar: string[] = [];
    let palavrasEncontradas: string[] = [];
    let pontuacao = 0;
    let tempo = 0;
    let intervalo: any;

    let nomeUsuario: string = '';
    let nomeArmazenado: string | null = localStorage.getItem('nomeUsuario');
    let telaLogin = !nomeArmazenado;

    let ranking: { nome: string; pontuacao: number }[] = JSON.parse(localStorage.getItem('ranking') || '[]');

    function extrairPalavrasPrincipais(texto: string) {
        const palavrasUnicas = new Set(
            texto
                .toLowerCase()
                .replace(/[.,]/g, '')
                .split(' ')
                .filter((palavra) => palavra.length > 4)
        );
        return Array.from(palavrasUnicas).slice(0, 6);
    }

    function iniciarJogo() {
        texto = textos[indiceAtual];
        palavrasEncontradas = [];
        palavrasParaEncontrar = extrairPalavrasPrincipais(texto);
        pontuacao = 0;
        tempo = 0;
        clearInterval(intervalo);
        intervalo = setInterval(() => tempo++, 1000);
    }

    onMount(() => {
        if (!telaLogin) {
            nomeUsuario = nomeArmazenado!;
            iniciarJogo();
        }
    });

    function selecionarTexto() {
        const selecao = window.getSelection();
        const textoSelecionado = selecao?.toString().trim().toLowerCase();
        if (textoSelecionado && palavrasParaEncontrar.includes(textoSelecionado) && !palavrasEncontradas.includes(textoSelecionado)) {
            palavrasEncontradas = [...palavrasEncontradas, textoSelecionado];
            pontuacao += 10;
        }
        selecao?.removeAllRanges();
    }

    $: if (palavrasEncontradas.length === palavrasParaEncontrar.length) {
        clearInterval(intervalo);
        salvarRanking();
    }

    function proximoTexto() {
        indiceAtual = (indiceAtual + 1) % textos.length;
        iniciarJogo();
    }

    function entrarNoJogo() {
        if (nomeUsuario.trim().length > 0) {
            localStorage.setItem('nomeUsuario', nomeUsuario);
            telaLogin = false;
            iniciarJogo();
        }
    }

    function salvarRanking() {
        ranking.push({ nome: nomeUsuario, pontuacao });
        ranking.sort((a, b) => b.pontuacao - a.pontuacao);
        ranking = ranking.slice(0, 10); // top 10
        localStorage.setItem('ranking', JSON.stringify(ranking));
    }

    function deslogar() {
        localStorage.removeItem('nomeUsuario');
        telaLogin = true;
        nomeUsuario = '';
        clearInterval(intervalo);
    }
</script>

<style>
    body {
        background: linear-gradient(to right, #e0f7fa, #ffffff);
        font-family: 'Segoe UI', sans-serif;
        margin: 0;
        height: 100vh;
        display: flex;
        justify-content: center;
        align-items: center;
    }

    .container {
        display: flex;
        flex-direction: column;
        align-items: center;
        justify-content: center;
        gap: 1.5rem;
        margin: auto;
        max-width: 900px;
    }

    .aero-box {
        background: rgba(255, 255, 255, 0.25);
        box-shadow: 0 8px 32px 0 rgba(31, 38, 135, 0.37);
        backdrop-filter: blur(8px);
        -webkit-backdrop-filter: blur(8px);
        border-radius: 10px;
        padding: 1rem 2rem;
        width: 100%;
        color: black;
    }

    .texto-jogo {
        font-size: 1.2rem;
        cursor: text;
        user-select: text;
    }

    .palavras-encontradas {
        color: green;
        font-weight: bold;
    }

    .botoes {
        display: flex;
        gap: 1rem;
    }

    button {
        padding: 0.5rem 1rem;
        border: none;
        background: #00796b;
        color: white;
        border-radius: 5px;
        cursor: pointer;
    }

    button:hover {
        background: #004d40;
    }

    .sair-btn {
        align-self: flex-end;
        margin-bottom: 0.5rem;
        background: #e53935;
    }

    .sair-btn:hover {
        background: #b71c1c;
    }

    h2 {
        margin-bottom: 0.5rem;
    }

    ul {
        list-style: none;
        padding: 0;
        display: flex;
        flex-wrap: wrap;
        gap: 0.5rem;
        justify-content: center;
    }

    li {
        background-color: rgba(255, 255, 255, 0.5);
        padding: 0.4rem 0.8rem;
        border-radius: 5px;
        color: black;
        font-weight: bold;
    }

    li.encontrada {
        color: green;
        background-color: rgba(200, 255, 200, 0.6);
    }

    .login-container {
        display: flex;
        flex-direction: column;
        align-items: center;
        gap: 1rem;
        background: rgba(255, 255, 255, 0.25);
        backdrop-filter: blur(10px);
        padding: 2rem;
        border-radius: 10px;
        box-shadow: 0 8px 32px 0 rgba(31, 38, 135, 0.37);
    }

    input[type="text"] {
        padding: 0.5rem;
        border: none;
        border-radius: 5px;
        width: 200px;
    }

    .ranking {
        background-color: rgba(255, 255, 255, 0.5);
        padding: 1rem;
        border-radius: 10px;
        max-width: 300px;
        width: 100%;
    }

    .ranking h3 {
        margin-top: 0;
    }
</style>

{#if telaLogin}
    <div class="container">
        <div class="login-container">
            <h2>Bem-vindo ao Caça-Palavras!</h2>
            <p>Digite seu nome para começar:</p>
            <input type="text" bind:value={nomeUsuario} placeholder="Seu nome" />
            <button on:click={entrarNoJogo}>Entrar</button>
        </div>
    </div>
{:else}
    <div class="container">
        <button class="sair-btn" on:click={deslogar}>Sair</button>
        <div class="aero-box texto-jogo" on:mouseup={selecionarTexto}>
            <p><strong>Jogador:</strong> {nomeUsuario}</p>
            <p>{texto}</p>
        </div>

        <div class="aero-box">
            <h2>Palavras para encontrar</h2>
            <ul>
                {#each palavrasParaEncontrar as palavra}
                    <li class={palavrasEncontradas.includes(palavra) ? 'encontrada' : ''}>{palavra}</li>
                {/each}
            </ul>
        </div>

        <div class="aero-box">
            <p><strong>Pontuação:</strong> {pontuacao}</p>
            <p><strong>Tempo:</strong> {tempo}s</p>
            <div class="botoes">
                <button on:click={proximoTexto}>Próximo Texto</button>
                <button on:click={iniciarJogo}>Reiniciar</button>
            </div>
        </div>

        <div class="aero-box ranking">
            <h3>🏆 Ranking (Top 10)</h3>
            <ol>
                {#each ranking as item}
                    <li>{item.nome} - {item.pontuacao} pts</li>
                {/each}
            </ol>
        </div>
    </div>
{/if}