<script lang="ts">
  import Sidebar from "$lib/components/sidebar.svelte";
  import type { Page } from "$lib/types";
  
  let page: Page = $state("about");

  const setPage = (p: Page) => {
    page = p;
  }

</script>


<main>
  <div id="nav">
    <Sidebar setPage={setPage}/>
  </div>

  <div id="content">
    <div id="c__upper">

    </div>

    <div id="c__lower">
    </div>
  </div>
</main>


<style lang="scss">
  @use "../styles/globals";

  main {
    width: 100vw;
    height: 100vh;

    display: flex;
    flex-direction: row;
  }

  #nav {
    width: 20%; height: 100%;

    display: flex;
    flex-direction: column;
  }

  #content {
    width: 80%; height: 100%;

    display: flex;
    flex-direction: column;
  }

  #c__upper {
    height: 35%; width: 100%;
  }

  #c__lower {
    --cpadding: calc(var(--margin) * 8);
    height: 65%;

    padding: var(--cpadding);
  }

</style>