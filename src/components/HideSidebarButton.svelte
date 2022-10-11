<script lang="ts">
  let sidebarIsHidden = false
  export let handleHideSideBar: any

  function hideSidebar(e: any): void {
    const app = document.querySelector(".app");

    app?.classList.toggle("sidebar");

    handleHideSideBar()
    sidebarIsHidden = !sidebarIsHidden

    if (sidebarIsHidden) e.target.style.opacity = '0.5'
    else e.target.style.opacity = '1'
  }
</script>

<button on:click={hideSidebar}>
{#if sidebarIsHidden}
    Show
  {:else}
    Hide
{/if}
</button>

<style>
  button {
    bottom: 1rem;
    left: 1rem;
    position: absolute;
    padding: .5em 1em;
    border-radius: 7px;
    transition: all ease 250ms;
    color: var(--light);

  }

  button:hover {
    opacity: 1 !important;
    background-color: rgba(0, 0, 0, 0.5);
  }
</style>
