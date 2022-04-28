<script>
    import Spinner from "./Spinner.svelte";
    import Results from "./Results.svelte";
    import Search from "./Search.svelte";
    import { promise } from "./stores.js";

    let darkmode = false;

function toggleTheme() {
    darkmode = !darkmode;
}
</script>
<!-- Navigator -->
<nav class="navigator">
    <a href="https://www.youtube.com/watch?v=dQw4w9WgXcQ&ab_channel=RickAstley" class="w3-button w3-bar-item">Home</a>
    <a href="https://minesweeperonline.com/#200-night" class="w3-button w3-bar-item">Gmail</a>
    <a href="https://c.tenor.com/0dGpRmwd1P0AAAAC/weenor-memes-meme-funny-hotdog-glizzy-haha-weiner-cursed.gif" class="w3-button w3-bar-item">Picture</a>
    <a href="https://c.tenor.com/EJ2mIpyaRk0AAAAd/snicker_doodle7-chips.gif" class="w3-button w3-bar-item">Contact</a>
    <a href="https://www.nytimes.com/games/wordle/index.html" class="w3-button w3-bar-item">Wordle</a>

    <label class="switch">
      <input on:change={toggleTheme} type="checkbox" checked>
      <span class="slider round"></span>
    </label>
</nav>

<main class:darkmode >
  <div class="grid-container">
  <div class="grid-item">
  <!-- Logo -->
    <img src="./ass.png" alt=""> 
    
    <!-- Sökmotor -->
    <Search/>
  </div>
  <div class="grid-item">
    {#await $promise}
        <Spinner />
    {:then result}
        <Results json={result} />
    {:catch error}
        <p style="color: red">{error.message}</p>
    {/await}
  </div>
  </div>
</main>

<style>
    :global(body) {
        padding: 0;
        margin: 0;
        overflow: hidden;
    }
    

    main {
        height: 100vh;
        width: 100vw;
        background: linear-gradient(
            -45deg,
            #201600ad,
            #352400);
        display: flex;
        justify-content: start;
        align-items: center;
        flex-direction: column;
        gap: 50px;
        padding-top: 10%;
        padding-left: 10%;
        padding-right: 10%;
        padding-bottom: 5%;
        box-sizing: border-box;
        transition: gradient 10s ease;
    }
    .grid-container{
      display: grid;
      grid-template-columns: auto auto;
      padding: 10px;
    }
    .grid-item {
  text-align: center;
    }

    .navigator {
        overflow: hidden;
        background-color: #333;
    }
    .navigator a {
        float: left;
        color: #f2f2f2;
        text-align: center;
        padding: 14px 16px;
        text-decoration: none;
        font-size: 17px;
}
    .navigator a:hover {
  background-color: #ddd;
  color: black;
}

.darkmode{
  background: linear-gradient(
    -45deg,
    #a56941c0,
    #5a3a25);
}

.switch {
  position: relative;
  display: inline-block;
  width: 60px;
  height: 34px;
}

.switch input { 
  opacity: 0;
  width: 0;
  height: 0;
}

.slider {
  position: absolute;
  cursor: pointer;
  top: 0;
  left: 0;
  right: 0;
  bottom: 0;
  background:#ffffff;
  -webkit-transition: .4s;
  transition: .4s;
}

.slider:before {
  position: absolute;
  content: "";
  height: 26px;
  width: 26px;
  left: 4px;
  bottom: 4px;
  background:#a56941c0;  
  -webkit-transition: .4s;
  transition: .4s;
}

input:checked + .slider {
  background: linear-gradient(
    -90deg,
    #363636c9,
    #363636);}

input:focus + .slider {
  box-shadow: 0 0 1px #2196F3;
}

input:checked + .slider:before {
  -webkit-transform: translateX(26px);
  -ms-transform: translateX(26px);
  transform: translateX(26px);
}

/* Rounded sliders */
.slider.round {
  border-radius: 34px;
}

.slider.round:before {
  border-radius: 50%;
}

    @keyframes gradient {
        0% {
            background-position: 0% 50%;
        }
        50% {
            background-position: 100% 50%;
        }
        100% {
            background-position: 0% 50%;
        }
    }
</style>
