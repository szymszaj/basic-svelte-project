<script>
  let name = "";

  function greet() {
    alert(`Hello, ${name}!`);
  }
</script>

<main>
  <h1>Prosta Aplikacja Powitalna</h1>
  <label for="name">Wprowadź swoje imię:</label>
  <input type="text" bind:value={name} id="name">

  <button on:click={greet}>Powitaj</button>
</main>

<style>
  main {
    text-align: center;
    padding: 1em;
    max-width: 300px;
    margin: 0 auto;
  }

  h1 {
    color: #007acc;
    font-size: 2em;
  }

  label {
    display: block;
    margin-top: 1em;
  }

  input {
    width: 100%;
    padding: 0.5em;
    margin-top: 0.5em;
  }

  button {
    margin-top: 1em;
    padding: 0.5em;
    cursor: pointer;
  }
</style>
