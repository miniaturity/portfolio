<script lang="ts">
  import type { Page } from "$lib/types";

  let {
    setPage
  }: {
    setPage: (p: Page) => void,
  } = $props();

  interface Button {
    name: string,
    img: string,
    imgPos?: [number, number]
    onClick: () => void,
  }

  const buttons: Button[] = [
    {
      name: "about",
      img: "/",
      onClick: () => setPage("about")
    },
    {
      name: "projects",
      img: "?",
      onClick: () => setPage("projects")
    }
  ];

  const repeatedButtons = Array(2).fill(buttons).flat();
</script>

<nav>
  <div id="marq">
    <div class="marq-inner">
      {#each repeatedButtons as button}
        <button onclick={button.onClick}>
          {button.name}
        </button>
      {/each}
    </div>

    <div class="marq-inner" aria-hidden="true">
      {#each repeatedButtons as button}
        <button onclick={button.onClick}>
          {button.name}
        </button>
      {/each}
    </div>
  </div>
</nav>

<style lang="scss">
  @use "../../styles/globals";

  nav {
    width: 100%; height: 100%;

    position: relative;
    display: flex;
    flex-direction: column;
    align-items: center;

    --gap: calc(var(--margin) * 4);
    overflow: hidden;
  }

  #marq {
    --time: 24s;

    display: flex;
    flex-direction: column;

    gap: var(--gap);
    width: 70%; height: 100%;
   
  }

  .marq-inner {
    display: flex;
    flex-direction: column;
    gap: var(--gap);
    flex-shrink: 0;
  }

  button {
    width: 100%;
    aspect-ratio: 1 / 1;
    
    position: relative;
    display: flex;
    justify-content: flex-end; align-items: flex-end;
    
    font-family: nintendo;
    font-size: 2rem;
    text-align: end;

    padding: calc(var(--gap) / 2);

    &:hover {
      cursor: pointer;
    }
  }

</style>