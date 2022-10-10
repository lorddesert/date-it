<script lang="ts">
  import { onDestroy, onMount } from 'svelte';
  import HideSidebarButton from "./HideSidebarButton.svelte";
  import Link from "./Link.svelte";

  let canvas: HTMLTextAreaElement;
  let intervalCallback = setInterval(saveContent, 5000);
  let textAreaValue: string = JSON.parse(localStorage.getItem('note') || '')

  function saveContent(): void {
    const text = canvas.value

    if (!text) return

    localStorage.setItem("note", JSON.stringify(text));
    console.log("Message saved! 👌")

  }

  onMount(() => {
    
  });

  onDestroy(() => {
    clearInterval(intervalCallback)
  })
</script>

<main class="app sidebar">
  <aside>
    <section class="side-bar">
      <ul>
        <Link href="/editor" />
        <Link href="/notes" />
      </ul>
    </section>
    <section>
      <HideSidebarButton />
    </section>
  </aside>
  <textarea
    bind:this={canvas}
    value={textAreaValue}
    placeholder="Hi mama!"
    name="canvas"
    id="canvas"
    cols="30"
    rows="10"
  />
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
    font-family: "Oxygen Mono";
  }

  .sidebar {
    grid-template-columns: minmax(150px, 200px) 1fr;
  }

  aside {
    background-color: var(--app-bg);
    color: var(--light);
    padding: 0.5em;
    margin: 0.5em;
  }

  textarea {
    background-color: #051722;
    color: var(--light);
    font-size: var(--text-area-font-size);

    min-height: 100vh;
    width: 100%;
    padding: 3em;
    resize: none;
  }

  .hidden {
    display: none;
  }
</style>
