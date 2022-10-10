<script lang="ts">
  export let href: string = ''
  export let text: string = href.match(/\//gi)?.length === 1
    ? href.replace('/', '').charAt(0).toUpperCase() + href.slice(2)
    : href
</script>

<li>
  {#if href}
    <a {href}>{text}</a>
  {/if}
</li>

<style>
    li {
    border-radius: 7px;
    color: var(--light);
    background-color: var(--app-bg);
    transition: all ease 125sms;
    border-bottom: solid transparent 1px;
    border-radius: 7px 7px 0 0;
    position: relative;
  }

  li:not(:last-child) {
    margin-bottom: .25em;
  }

  li:before {
    content: '';
    position: absolute;
    border-bottom: 1px solid transparent;
    height: 1px;
    width: 1px;
    transition: all ease 240ms;
    bottom: 0;
  }

  li:hover {
    background-color: rgba(0, 0, 0, 0.5);
    border-radius: 7px 7px 0 0;
  }

  li:hover:before{
    width: 100%;
    border-bottom: solid greenyellow 1px;
  }

  a {
    display: block;
    padding: .5em;
    width: 100%;
  }
</style>