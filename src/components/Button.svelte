<script lang="ts">
  import { onDestroy, onMount } from "svelte";

  // Props
  export let value: string;
  export let click = () => alert("Boom!");

  //Variables and state
  const saveMessages = ["Done", "Nice!", "Well done!", "Good work!"];
  const randomIndex = () => Math.floor(Math.random() * saveMessages.length);
  let successMessage = "";
  let saveTimeOut: any;
  let done = false;

  //Functions
  function doClick() {
    done = true;
    click();

    if (saveTimeOut) clearTimeout(saveTimeOut);

    successMessage = saveMessages[randomIndex()];
    saveTimeOut = setTimeout(() => {
      done = false;
    }, 800);
  }

  function listenToSave(e: KeyboardEvent): void {
    const { ctrlKey, key } = e;

    if (ctrlKey && key === "s") {
      e.preventDefault();
      doClick();
    }
  }

  //Lifecycles
  onMount(() => {
    document.addEventListener("keydown", listenToSave);
  });

  onDestroy(() => {
    document.removeEventListener("keydown", listenToSave);
  });
</script>

<button on:click={doClick} class={done ? "success" : ""}>
  {#if done}
    {successMessage}
  {:else}
    {value}
  {/if}
</button>

<style>
  button {
    background-color: rgba(0, 0, 0, 0.5);
    border-radius: 7px;
    color: var(--light);
    min-width: 85px;
    padding: 0.5em;
    transition: 150ms all linear;
  }

  button:hover {
    box-shadow: 0 0 5px var(--aside-bg);
  }

  .success {
    background: rgba(172, 255, 47, 0.63);
  }

  /* button:hover {
    width: 100%;
    border-bottom: solid greenyellow 1px;
  } */
</style>
