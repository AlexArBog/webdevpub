<script>
  import { video_player_is_active } from "./stores.js";
  import { Button, Overlay } from "svelte-materialify";
  import { videos } from "./videos.js";
  import Player from "./Player.svelte";
  import Thumbnail from "./Thumbnail.svelte";

  let is_fullscreen = false;
</script>

<main>
  <div class="square">
    <img src="ass.videos.png" width=250 height=100 alt="Mega big juicy gay furry porn">
  </div>
  <div class="line"></div>
  <div class="topnav">
    <a class="active" href="#home">HOME</a>
    <a href="https://www.youtube.com/watch?v=fOI8bA3xEJU&ab_channel=CatersClips">VIDEOS</a>
    <a href="#contact">CATEGORIES</a>
    <a href="#about">CHANNELS</a>
    <a href="#about">FEET</a>
  </div>
  <div class="line2"></div>

  <div class="grid">
    {#each Array(20) as _, i}
        <!-- Probably here you want to show different videos than I have selected -->
        <Thumbnail video={videos[i%20]}> </Thumbnail>
    {/each}
  </div>
  <Overlay
    opacity={is_fullscreen ? 1 : 0.7}
    color="black"
    active={$video_player_is_active}
    on:click={() => {
      $video_player_is_active = false;
    }}
  >
    <div
      id="video"
      class:fullscreen={is_fullscreen == true}
      on:click={(e) => {
        e.stopPropagation();
      }}
    >
      <div id="close">
        <Button
          class="error-color"
          size="small"
          on:click={() => {
            $video_player_is_active = false;
          }}
        >
          Close
        </Button>
      </div>
      <div id="fullscreen">
        <Button
          size="small"
          class="primary-color"
          on:click={() => {
            is_fullscreen = !is_fullscreen;
            // do not focus the fullscreenbutton if clicked
            // this is because otherwise clicking space will cause
            // the video player to maximize/minimize instead of pause/play
            // when space is clicked
            if (document.activeElement != document.body)
              document.activeElement.blur();
          }}
        >
          {is_fullscreen ? "Minimize" : "Theatre Mode"}
        </Button>
      </div>

      {#if is_fullscreen}
        <div id="gigascreen">
          <Button
            size="small"
            class="secondary-color"
            on:click={() => {
              // do not focus the fullscreenbutton if clicked
              // this is because otherwise clicking space will cause
              // the video player to maximize/minimize instead of pause/play
              // when space is clicked
              if (document.activeElement != document.body)
                document.activeElement.blur();

              let div = document.getElementById("vid");
              if (div.requestFullscreen) div.requestFullscreen();
              else if (div.webkitRequestFullscreen)
                div.webkitRequestFullscreen();
              else if (div.msRequestFullScreen) div.msRequestFullScreen();
            }}
          >
            {"Gigascreen"}
          </Button>
        </div>
      {/if}

      <Player />
    </div>
  </Overlay>

  <src />
</main>

<style>
  :global(:root) {
    background: black;
    --netflix-red: #564833;
    --netflix-red-opacity: rgba(229, 9, 20, 0.3);
  }

  :global(body) {
    padding: 0;
    margin: 0;
  }

  main {
    min-height: 100vh;
    width: 100vw;
    
    box-sizing: border-box;
  }

  #video {
    position: fixed;
    transition: all 0.3s ease-out;
    left: 15%;
    right: 15%;
    top: 15%;
    bottom: 15%;
  }

  #video.fullscreen {
    left: 0%;
    right: 0%;
    top: 0%;
    bottom: 0%;
  }

  #video.fullscreen #gigascreen {
    position: absolute;
    top: 10px; /* position the top  edge of the element at the middle of the parent */
    left: 50%; /* position the left edge of the element at the middle of the parent */
    transform: translate(-50%, 0);
    z-index: 100;
  }
  #video #close {
    position: absolute;
    top: -10px;
    right: -10px;
    z-index: 100;
  }

  #video #fullscreen {
    position: absolute;
    top: -10px;
    left: -10px;
    z-index: 100;
  }

  #video.fullscreen #close {
    position: absolute;
    top: 10px;
    right: 10px;
    z-index: 100;
  }

  #video.fullscreen #fullscreen {
    position: absolute;
    top: 10px;
    left: 10px;
    z-index: 100;
  }

  .grid {
    position: absolute;
    margin-top: 170px;
    margin-left: 0px;
    display: grid;
    grid-row-gap: 100px;
    grid-column-gap: 10px;
    grid-template-columns: 150px 150px 150px 150px 150px;
    padding: 10px;
  }
  
@media only screen and (max-width: 850px) {
  .grid {
    grid-column-gap: 1px;
    grid-template-columns: 150px 150px 150px 150px;
  }
}

.square{
  z-index: 1;
  position: fixed;
  width: 100%;
  background-color:rgb(33, 33, 33);
}
.line{
  z-index: 1;
  position: fixed;
  background-color: rgb(54, 54, 54);
  width: 100%;
  height: 2px;
  margin-top: 100px;
}
.line2{
  z-index: 1;
  position: fixed;
  background-color: rgb(54, 54, 54);
  width: 100%;
  height: 2px;
  margin-top: 155px;
}

  .topnav {
  z-index: 1;
  overflow: hidden;
  position: fixed;
  width: 100%;
  margin-top:102px;
  background-color: rgb(23, 23, 23);
}

.topnav a {
  float: left;
  color: #f2f2f2;
  text-align: center;
  padding: 14px 16px;
  text-decoration: none;
  font-size: 17px;
}

.topnav a:hover {
  background-color: orange;
  color: black;
}
</style>
