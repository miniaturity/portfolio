<script lang="ts">
    import type { Component, Snippet } from "svelte";

    interface Tile {
        id: number;
        class?: string;
        style?: string;
        tag?: string;
        component?: Component;
        componentProps?: Record<string, any>;

        snippet?: Snippet<[any]>;
        snippetProps?: Record<string, any>;
    }

    function press(e: PointerEvent, id: number) {

    }

    function release(e: PointerEvent, id: number) {

    }

    const tileContents = {
        17: "1"
    }

    const tiles: Tile[] = [
        { id: 1, class: "tile sil-speaker" },
        { id: 2, class: "tile sil-minik" },
        { id: 3, class: "tile", style: "grid-row: 2; grid-column: 3", snippet: defaultTile},
        { id: 4, class: "tile", style: "grid-row: 2; grid-column: 4", snippet: defaultTile },
        { id: 5, class: "tile sil-screen", tag: "div" },

        { id: 6, class: "tile sil-big", style: "grid-row: 1 / 2; grid-column: 9 / 10" },
        { id: 7, class: "tile sil-big", style: "grid-row: 1 / 2; grid-column: 11 / 12" },
        { id: 8, class: "tile sil-big", style: "grid-row: 1 / 2; grid-column: 13 / 14" },
        { id: 9, class: "tile sil-big", style: "grid-row: 1 / 2; grid-column: 15 / 16" },

        { id: 10, class: "tile", style: "grid-row: 1; grid-column: 17", snippet: defaultTile },
        { id: 11, class: "tile", style: "grid-row: 2; grid-column: 17", snippet: defaultTile },

        ...Array.from({ length: 17 }, (_, i) => ({
            id: i + 12,
            class: "tile",
            style: `grid-row: 3; grid-column: ${i + 1}`, 
            snippet: defaultTile,
        })),

        ...Array.from({ length: 17 }, (_, i) => ({
            id: i + 29,
            class: "tile",
            style: `grid-row: 4; grid-column: ${i + 1}`, 
            snippet: defaultTile
        })),

        ...Array.from({ length: 3 }, (_, i) => ({
            id: i + 46,
            class: "tile",
            style: `grid-row: 5; grid-column: ${i + 1}`, 
            snippet: defaultTile
        })),

        { id: 49, class: "tile", style: "grid-row: 5; grid-column: 4 / 8;", tag: "div" },
        { id: 50, class: "tile", style: "grid-row: 5; grid-column: 8 / 11;", tag: "div" },
        { id: 51, class: "tile", style: "grid-row: 5; grid-column: 11 / 15;", tag: "div" },
        { id: 52, class: "tile", style: "grid-row: 5; grid-column: 15 / 18;", tag: "div" },

        ...Array.from({ length: 17 }, (_, i) => ({
            id: i + 53,
            class: "tile",
            style: `grid-row: 6; grid-column: ${i + 1}`, 
            snippet: defaultTile
        })),
    ];

</script>

{#snippet defaultTile(content: string = "", texture?: string)}
    <div class="tile-in">
        {content}
        {#if texture}
            <img src={texture} alt=""/>
        {/if}
    </div>
{/snippet}

<div class="synth">
    <div class="s-inner">
        <div class="si-l">
            {#each tiles as tile}
                <svelte:element
                    this={tile.tag || "button"}
                    class={tile.class}
                    id={`t_${tile.id}`}
                    style={tile.style}
                    aria-label="tile"

                    role={tile.tag === "div" ? "button" : undefined}
                    tabindex={tile.tag === "div" ? 0 : undefined}

                    onpointerdown={(e) => press(e, tile.id)}
                    onpointerup={(e) => release(e, tile.id)}
                >
                    {#if tile.component}
                        <tile.component {...tile.componentProps}/>
                    {/if}

                    {#if tile.snippet}
                        {@render tile.snippet({ ...tile.snippetProps })}
                    {/if}
                </svelte:element>
            {/each}
        </div>
        <div class="si-r">

        </div>
    </div>
</div>

<style lang="scss">
    :global(*) {
        box-sizing: border-box;
    }

    .synth {
        --border: 1px solid #000;
        --width: clamp(400px, 50vw, 900px);
        --s1p: calc(var(--width) * 0.01);
        --br: calc(1.75 * var(--s1p));
        --bg: #353535;

        width: var(--width);
        aspect-ratio: 45 / 16;
        border: var(--border);
        border-radius: var(--br);
        background-color: var(--bg);

        display: flex;
        justify-content: center;
        align-items: center;
    }

    .s-inner {
        --pad: calc(var(--s1p) * 1.5);
        width: calc(100% - calc(var(--pad) * 2)); height: calc(100% - calc(var(--pad) * 2));
    }

    .si-l {
        --i-br: calc(var(--br) / 3);
        --i-bg: #464646;

        width: 95%; height: 100%;
        border: var(--border);
        border-radius: var(--i-br);

        display: grid;
        grid-template-columns: repeat(17, 1fr);
        grid-template-rows: repeat(6, 1fr);
    }

    .tile {
        cursor: pointer;
        width: 100%;
        height: 100%;

        border-radius: var(--i-br);
        border: var(--border);
        background: linear-gradient(to bottom, var(--i-bg), color-mix(in oklab, var(--i-bg), black 20%));
        padding: 0;
    }

    .tile-in {
        position: relative;
        width: 100%; height: 100%;
        &:after {
            content: '';
            position: absolute;
            top: 7.5%; left: 7.5%;
            width: 85%; height: 85%;
            border-radius: 100%;
            background: linear-gradient(to top, var(--i-bg), color-mix(in oklab, var(--i-bg), black 20%));
        }
    }

    .sil-speaker {
        width: 200%;
        height: 200%;
        grid-column: 1 / 2;
        grid-row: 1 / 2;
    }

    .sil-minik {
        width: 200%;
        height: 100%;
        grid-column: 3 / 4;
        grid-row: 1;
    }

    .sil-screen {
        cursor: default;
        grid-row: 1 / 2; 
        grid-column: 5 / 9;
        width: 100%;
        height: 200%;
        background: #000;
    }

    .sil-big {
        width: 200%;
        height: 200%;
    }

    .contain {
        cursor: default;
    }
</style>