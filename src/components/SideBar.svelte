<script lang="ts">
  import HideSidebarButton from "./HideSidebarButton.svelte";
  import Link from "./Link.svelte";
  import { fade } from "svelte/transition";

  let showSidebar: boolean = false;

  const handleHideSideBar = () => (showSidebar = !showSidebar);
  $: console.log(showSidebar);

</script>

{#if !showSidebar}
  <aside out:fade>
    <section class={`side-bar ${!showSidebar && "hidden"}`}>
      <ul>
        <Link href="/editor" />
        <Link href="/notes" />
      </ul>
    </section>
  </aside>
{/if}
<HideSidebarButton {handleHideSideBar} />

<style>
  .sidebar {
    grid-template-columns: minmax(150px, 200px) 1fr;
  }

  aside {
    background-color: var(--app-bg);
    color: var(--light);
    padding: 0.5em;
    margin: 0.5em;
  }
</style>
