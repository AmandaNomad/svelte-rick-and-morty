<script>
  import Character from "./libs/Character.svelte";
  let characters = []; //declara una variable e inicializa su valor como arreglo vacio
  let page = 1;
  async function loadCharacters() {
    //se declara la funcion loadCharacters con aync (esto indica que esta funcion contendra operaciones asincronas y que se puede utilizar la palabra await para esperar a que se completen las operaciones)
    const response = await fetch(
      "https://rickandmortyapi.com/api/character?page=" + page
    ); //hace una solicitud http utilizando la funcion fetch para obtener datos de la url. El await se utiliza para esperar la respuesta de la solicitud antes de continuar con la ejecucion del codigo.
    const data = await response.json(); //Aquí, se utiliza await nuevamente para esperar a que se complete la operación de análisis de la respuesta en formato JSON. La respuesta JSON se almacena en la variable data
    console.log(data); //Esta línea imprime los datos obtenidos de la API en la consola del navegador.
    characters = data.results; //Aquí, se asigna la propiedad results de data a la variable characters. En este punto, characters contendrá la lista de personajes obtenidos de la API.
  }

  loadCharacters(); //se llama para iniciar la carga de los personajes desde la API

  function paginaSiguiente() {
    page++;
    loadCharacters();
  }
  function paginaAnterior() {
    page--;
    loadCharacters();
  }
</script>

<h1 class="title">Rick and Morty Svelte</h1>


<div class="container">

  <div class="btns">
    <button class="btn btn-info btn-lg" on:click={paginaAnterior} disabled={page === 1}>Anterior</button>
    <button class="btn btn-info btn-lg" on:click={paginaSiguiente}>Siguiente</button>
  </div>
  <div class="grid">
    <!-- each se utiliza en svelte para crear un bucle que recorre una lista de elementos almacenada en la variable characters
  character se utiliza para representar cada elemento individual de la lista. Se recorre la lista characters y para cada character se crea un div-->
    {#each characters as character}
      <Character {character} />
    {/each}
  </div>
</div>
