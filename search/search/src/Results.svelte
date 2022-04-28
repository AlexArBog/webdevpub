<script>
    export let json;
    import { fly, fade, slide, draw } from "svelte/transition";
</script>

<main>
    {#if json && "data" in json && "items" in json.data && json.data.items.length > 0}
        <div id="item-holder">
            {#each json.data.items as item}
                <div id="item">
                    <br>
                    <p id="url">{item.url} - {item.author}</p>
                    <br>
                    <p id="name">{item.name}</p>
                    <br>
                    <p id="published">{item.published_at}</p>
                    <br>
                    {#each Object.entries(item) as [key, value]}
                        <!--<p in:fade>{key + " : " + JSON.stringify(value)}</p>-->
                    {/each}
                </div>
            {/each}
        </div>
    {:else if json}
        <div>
            <h2 in:fade>Fann ingen {JSON.stringify(json.data.q)}</h2>
        </div>
    {/if}
</main>

<style>
    #item-holder {
        -ms-overflow-style: none; /* for Internet Explorer, Edge */
        scrollbar-width: none; /* for Firefox */
        overflow-y: scroll;
    }

    #item-holder::-webkit-scrollbar {
        display: none; /* for Chrome, Safari, and Opera */
    }

    main {
        overflow: auto;
        height: 30vw;
    }

    #item-holder {
        border-radius: 25px;
        display: flex;
        justify-content: start;
        align-items: center;
        flex-direction: column;
        overflow-y: scroll;
        box-sizing: border-box;
        padding-left: 10%;
        padding-right: 10%;
        max-width: 100%;
        row-gap: 20px;
    }

    #item {
        border-radius: 25px;
        background-color: rgba(245, 245, 245, 0.329);
        border: 2px solid rgb(0, 0, 0);
        width: 100%;
        box-sizing: border-box;
        word-wrap: break-word;
    }

    p {
        color: rgba(255, 255, 255, 0.806);
        text-align: left;
        margin-bottom: -10px;
        margin-top: -10px;
        margin-left: 10px;
    }
    h2 {
        color: rgba(255, 255, 255, 0.806);
    }

    #name{
        font-size: 20px;
        color: #4a380f;
    }

    /** https://onaircode.com/html-css-custom-scrollbar-examples/ */
    ::-webkit-scrollbar {
        width: 15px;
        height: 15px;
    }
    ::-webkit-scrollbar-track {
        border-radius: 10px;
        background-color: rgba(255, 255, 255, 0.703);
    }
    ::-webkit-scrollbar-thumb {
        background-image: linear-gradient(45deg, #4a380f, #544e0d80);
        border-radius: 10px;
        -webkit-box-shadow: rgba(57, 57, 57, 0.699) 0 3px 13px 1px;
    }
    @media only screen and (max-width: 870px) {
        .grid-container{
            display: flex;
            flex-direction: column;
            column-gap: 1em;
            height: 100%;
            padding: 1em;
        }
    }
</style>
