<script lang="ts">
    import Synth from "$lib/components/synth.svelte";

</script>

<main>

    <header>
        miniaturity.com
    </header>

    <div class="synth-container">
        <Synth />
    </div>
</main>

<style lang="scss">
    :global(body) {
        margin: 0; padding: 0;
    }
    main {
        margin: 0; padding: 0;
        width: 100vw;
        height: 100vh;

        display: flex;
        justify-content: center;
        align-items: center;
    }

    header {
        position: absolute;
        --fs: clamp(1rem, 10vw, 6rem);

        font-family: "TE-20";
        font-size: var(--fs);
        top: var(--fs);

        user-select: none;
    }

   



    @font-face {
        font-family: "TE-20";
        src: url("$lib/assets/fonts/TE-20.ttf");
    }
</style>