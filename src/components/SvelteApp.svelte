<script lang='ts'>
  import SideBar from './SideBar.svelte';
  import { onDestroy, onMount } from 'svelte';
  import Button from './Button.svelte'

  let canvas: HTMLTextAreaElement;
  let intervalCallback = setInterval(saveContent, 5000);
  let textAreaValue: string = JSON.parse(localStorage.getItem('note') || '');

  function saveContent(): void {
    const text = canvas.value;

    if (!text) return;

    localStorage.setItem('note', JSON.stringify(text));
    console.log('Message saved! 👌');
  }

  onDestroy(() => {
    clearInterval(intervalCallback);
  });
</script>

<main class='app sidebar'>
  <SideBar />
  <div class='editor'>
    <textarea
      bind:this={canvas}
      value={textAreaValue}
      placeholder='Hi mama!'
      name='canvas'
      id='canvas'
      cols='30'
      rows='10'
    />
    <footer>
      <Button value='Save note' click={saveContent} />
      <Button value='No se' />
    </footer>
  </div>
</main>

<style>
  :root {
    --app-bg: #06283d;
    --aside-bg: #256d85;
    --highlight: #47b5ff;
    --light: #dff6ff;
    --text-area-font-size: 1rem;
    --app-font-size: 1rem;
  }

  main {
    font-size: var(--app-font-size);
    display: grid;
    grid-template-columns: 1fr;
    background-color: var(--app-bg);
    font-family: 'Oxygen Mono';
    min-height: 100vh;
  }

  .editor {
    display: grid;
    grid-template-rows: 1fr auto;
    background-color: #051722;
  }

  .editor footer {
    padding: .5em;
  }

  .sidebar {
    grid-template-columns: minmax(150px, 200px) 1fr;
  }

  textarea {
    color: var(--light);
    font-size: var(--text-area-font-size);
    background-color: inherit;
    width: 100%;
    padding-top: 50px;
    padding-left: 3em;
    resize: none;
  }

  textarea:focus-visible {
    border: none;
    outline: none;
  }

  .hidden {
    display: none;
  }
</style>
