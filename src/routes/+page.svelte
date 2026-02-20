<script>
  let text = $state("");

  const dictionary = [
    { frase: "si la ia llegará", tipo: "IA" },
    { frase: "impacto de la ia", tipo: "IA" },
    { frase: "la ia ha venido para quedarse", tipo: "IA" },
    { frase: "cambiará tal y como lo conocemos", tipo: "IA" },
    { frase: "escribiendo sistemas completos", tipo: "IA" },
    { frase: "hay un patrón claro", tipo: "IA" },
    { frase: "el reto actual ya no es si", tipo: "IA" },
    { frase: "obsoletos en meses", tipo: "IA" },
    { frase: "mantiene estancado", tipo: "IA" },
    { frase: "la realidad corporativa", tipo: "IA" },
    { frase: "cambiar el juego", tipo: "IA" },
    { frase: "mientras todo", tipo: "IA" },
    { frase: "tu propio cliente", tipo: "curso" },
    { frase: "monetiza tu marca", tipo: "curso" },
    { frase: "monta tu negocio online", tipo: "curso" },
    { frase: "vive de internet", tipo: "curso" },
    { frase: "romper el status quo", tipo: "curso" },
    { frase: "en los comentarios", tipo: "curso" },
    { frase: "mente de tiburón", tipo: "curso" },
  ];

  const removeAccents = (str) => {
    return str.normalize("NFD").replace(/[\u0300-\u036f]/g, "");
  };

  let detected = $derived(
    dictionary.filter((item) => {
      const cleanPhrase = removeAccents(item.frase);
      const regex = new RegExp(cleanPhrase, "gi");

      return regex.test(removeAccents(text))
    }),
  );
</script>

<svelte:head>
  <title>Detector de Humo</title>
  <meta name="description" content="Comprueba si ese post de LinkedIn tiene información relevante o es una cuñadez escrita por un vendehumos." />
  
  <meta property="og:title" content="Detector de Humo 😶‍🌫️" />
  <meta property="og:description" content="Analizador de cuñadeces y vendehumos de LinkedIn." />
</svelte:head>

<main
  class="min-h-screen flex flex-col items-center py-20 px-4 gap-12"
>
  <h1 class="text-3xl sm:text-4xl font-extrabold text-cyan-400">Vale la pena?</h1>

  <div class="sm:text-xl text-slate-300">
    <p class="mb-2">
      Sospechas que el post pueda haber sido escrito por un gurú de la IA o un vendehumos?
    </p>
    <p>Comprueba si el post tiene información relevante o no vale la pena perder el tiempo.</p>
  </div>

  <textarea
    class="w-full max-w-2xl h-44 p-6 rounded-xl border border-slate-600 focus:border-cyan-400 focus:ring-cyan-400 bg-slate-800 text-slate-300 placeholder:text-slate-500 sm:text-xl" bind:value={text}
    placeholder="Pega el texto aquí"
  ></textarea>
  {#if detected.length > 0}
    <div class="w-full max-w-2xl bg-red-900/40 border border-red-500 p-6 rounded-xl">
      <h2 class="sm:text-xl font-bold mb-4 text-red-400">ALERTA DE HUMO DETECTADA 😶‍🌫️</h2>
      <ul class="space-y-2">
        {#each detected as item (item.frase)}
          <li class="flex items-center gap-2 text-red-200">
            <span class="bg-red-500/20 px-2 py-1 rounded text-sm border border-red-500/50 uppercase font-bold min-w-20">
              {item.tipo}
            </span>
            <span>Cuñadez: <strong class="text-white">"{item.frase}"</strong></span>
          </li>
        {/each}
      </ul>
    </div>
  {:else if text.length > 10}
    <div class="text-green-500 font-mono text-sm">
      Texto aparentemente limpio...
    </div>
  {/if}
</main>
