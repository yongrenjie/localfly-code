<script lang="ts">
    import { fly } from "svelte/transition";

    let novels = [
        {
            title: "Emma",
            opening:
                "Emma Woodhouse, handsome, clever, and rich, with a comfortable home and happy disposition, seemed to unite some of the best blessings of existence; and had lived nearly twenty-one years in the world with very little to distress or vex her.",
        },
        {
            title: "The Great Gatsby",
            opening:
                "In my younger and more vulnerable years my father gave me some advice that I've been turning over in my mind ever since.",
        },
        {
            title: "Mrs Dalloway",
            opening: "Mrs Dalloway said she would buy the flowers herself.",
        },
        {
            title: "The Catcher in the Rye",
            opening:
                "If you really want to hear about it, the first thing you'll probably want to know is where I was born, and what my lousy childhood was like, and how my parents were occupied and all before they had me, and all that David Copperfield kind of crap, but I don't feel like going into it, if you want to know the truth.",
        },
    ];

    let index = 0;
    function nextNovel() {
        index = index + 1;
    }
    function previousNovel() {
        index = index - 1;
    }
</script>

<main>
    <div id="middle">
        <div id="controls">
            <button on:click={previousNovel} disabled={index === 0}>←</button>
            <select bind:value={index}>
                {#each novels as novel, i}
                    <option value={i}>{novel.title}</option>
                {/each}
            </select>
            <button on:click={nextNovel} disabled={index === novels.length - 1}
                >→</button
            >
        </div>
        {#each novels as novel, i}
            {#if i === index}
                <p id="opening" transition:fly={{ x: 500 }}>{novel.opening}</p>
            {/if}
        {/each}
    </div>
</main>

<style>
    main {
        display: flex;
        justify-content: center;
        background-color: #ffe6f4;
        padding: 20px;
    }
    div#middle {
        background-color: #fcbaff;
        border: 2px solid #e688eb;
        padding: 10px;
        width: 300px;
    }
    div#controls {
        display: flex;
        justify-content: space-between;
        align-items: baseline;
    }
    p#opening {
        margin-bottom: 0;
    }
</style>
