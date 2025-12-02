<script lang="ts">

</script>


<main>
  <nav>
    <!-- sidebar -->
  </nav>

  <div id="content">
    <div id="c__upper">
      <!-- upper (pfp/sq) -->
    </div>

    <div id="c__lower">
    </div>
  </div>
</main>


<style lang="scss">
  @use "../styles/globals";

  :global(:root) {
    --margin: 4px;
  }

  main {
    width: 100vw;
    height: 100vh;

    display: flex;
    flex-direction: row;
  }

  nav {
    width: 30%; height: 100%;

    display: flex;
    flex-direction: column;
    background-color: green;
  }

  #content {
    width: 70%; height: 100%;

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