<script lang="ts">
	import { onMount } from 'svelte';

	let texto =
		"A energia solar e a energia eólica são fontes de energia limpa. O uso de energia renovável é essencial para reduzir as emissões de carbono.";

	const palavrasParaEncontrar = ["energia", "solar", "eólica", "limpa", "renovável", "carbono"];
	let palavrasEncontradas: string[] = [];

	let pontuacao = 0;
	let tempo = 0;
	let intervalo: any;

	// Iniciar o cronômetro ao montar o componente
	onMount(() => {
		intervalo = setInterval(() => tempo++, 1000);
	});

	// Parar cronômetro quando todas as palavras forem encontradas
	$: if (palavrasEncontradas.length === palavrasParaEncontrar.length) {
		clearInterval(intervalo);
	}

	// Função para verificar se o texto selecionado é uma palavra válida
	function verificarSelecao() {
		const selecionadoBruto = window.getSelection()?.toString().trim().toLowerCase();

		if (!selecionadoBruto) return;

		const selecionado = selecionadoBruto
			.normalize('NFD')
			.replace(/[\u0300-\u036f]/g, '') // Remove acentos
			.replace(/[.,!?;:]/g, ''); // Remove pontuação

		for (const palavra of palavrasParaEncontrar) {
			const palavraNormalizada = palavra
				.normalize('NFD')
				.replace(/[\u0300-\u036f]/g, '');

			if (selecionado === palavraNormalizada && !palavrasEncontradas.includes(palavra)) {
				palavrasEncontradas = [...palavrasEncontradas, palavra];
				pontuacao += 10;
			}
		}
	}

	// Verifica se uma palavra já foi encontrada
	function palavraJaEncontrada(palavra: string) {
		return palavrasEncontradas.includes(palavra);
	}

	// Função para destacar visualmente as palavras no texto
	function destacarTexto(texto: string): string {
		let resultado = texto;

		for (const palavra of palavrasParaEncontrar) {
			const encontrado = palavrasEncontradas.includes(palavra);
			const classe = encontrado ? "encontrada animada" : "para-encontrar";

			const regex = new RegExp(`\\b(${palavra})\\b`, 'gi');
			resultado = resultado.replace(regex, `<span class="${classe}">$1</span>`);
		}

		return resultado;
	}
</script>

<style>
	.container {
		display: flex;
		gap: 2rem;
		padding: 2rem;
		flex-wrap: wrap;
	}

	.texto {
		width: 60%;
		border: 1px solid #ccc;
		padding: 1rem;
		cursor: text;
		user-select: text;
		line-height: 1.6;
		font-size: 1.1rem;
	}

	.tabela {
		width: 30%;
	}

	.encontrada {
		background-color: yellow;
		font-weight: bold;
	}

	.para-encontrar {
		background-color: transparent;
	}

	.encontrada-lista {
		color: green;
		text-decoration: line-through;
		font-weight: bold;
	}

	.lista-palavras li {
		margin-bottom: 0.5rem;
		font-size: 1.1rem;
	}

	.pontuacao {
		margin-top: 1rem;
		font-size: 1.2rem;
		font-weight: bold;
	}

	.tempo {
		margin-top: 0.5rem;
		font-size: 1rem;
		color: #555;
	}

	.animada {
		animation: flash 0.5s ease-in-out;
	}

	@keyframes flash {
		0% {
			background-color: yellow;
		}
		50% {
			background-color: orange;
		}
		100% {
			background-color: yellow;
		}
	}
</style>

<div class="container" on:mouseup={verificarSelecao}>
	<div class="texto">
		{@html destacarTexto(texto)}
	</div>

	<div class="tabela">
		<h3>Palavras para encontrar</h3>
		<ul class="lista-palavras">
			{#each palavrasParaEncontrar as palavra}
				<li class:encontrada-lista={palavraJaEncontrada(palavra)}>
					{palavra}
				</li>
			{/each}
		</ul>

		<div class="pontuacao">Pontuação: {pontuacao}</div>
		<div class="tempo">Tempo: {tempo} segundos</div>
	</div>
</div>

