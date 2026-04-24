<script lang="ts">
    interface Tile {
        id: number;
        class?: string;
        style?: string;
        tag?: string;
    }

    function press(e: PointerEvent, id: number) {

    }

    function release(e: PointerEvent, id: number) {

    }

    const tiles: Tile[] = [
        { id: 1, class: "tile sil-speaker" },
        { id: 2, class: "tile sil-minik" },
        { id: 3, class: "tile", style: "grid-row: 2; grid-column: 3" },
        { id: 4, class: "tile", style: "grid-row: 2; grid-column: 4" },
        { id: 5, class: "tile sil-screen", tag: "div" },

        { id: 6, class: "tile sil-big", style: "grid-row: 1 / 2; grid-column: 9 / 10" },
        { id: 7, class: "tile sil-big", style: "grid-row: 1 / 2; grid-column: 11 / 12" },
        { id: 8, class: "tile sil-big", style: "grid-row: 1 / 2; grid-column: 13 / 14" },
        { id: 9, class: "tile sil-big", style: "grid-row: 1 / 2; grid-column: 15 / 16" },

        { id: 10, class: "tile", style: "grid-row: 1; grid-column: 17" },
        { id: 11, class: "tile", style: "grid-row: 2; grid-column: 17" },

        ...Array.from({ length: 17 }, (_, i) => ({
            id: i + 12,
            class: "tile",
            style: `grid-row: 3; grid-column: ${i + 1}`
        })),

        ...Array.from({ length: 17 }, (_, i) => ({
            id: i + 29,
            class: "tile",
            style: `grid-row: 4; grid-column: ${i + 1}`
        })),

        ...Array.from({ length: 3 }, (_, i) => ({
            id: i + 46,
            class: "tile",
            style: `grid-row: 5; grid-column: ${i + 1}`
        })),

        { id: 49, class: "tile", style: "grid-row: 5; grid-column: 4 / 8;" },
        { id: 50, class: "tile", style: "grid-row: 5; grid-column: 8 / 11;" },
        { id: 51, class: "tile", style: "grid-row: 5; grid-column: 11 / 15;" },
        { id: 52, class: "tile", style: "grid-row: 5; grid-column: 15 / 18;" },

        ...Array.from({ length: 17 }, (_, i) => ({
            id: i + 53,
            class: "tile",
            style: `grid-row: 6; grid-column: ${i + 1}`
        })),
    ];

</script>

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
                    <div class="t-in"></div>
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
        background-color: var(--i-bg);
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
        background-color: #000;
    }

    .sil-big {
        width: 200%;
        height: 200%;
    }

    .contain {
        cursor: default;
    }
</style>