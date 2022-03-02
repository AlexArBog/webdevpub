<script>
import { tick } from "svelte";
import { spring, tweened } from "svelte/motion";


        class clock{
        constructor(h, m){
            if (h <= 23 && h >= 0){
                this.h = h;
            }
            else{
                throw Error("Error: hour value must be >= 0 and < 24")
            }
            if (m < 60 && m >= 0){
                this.m = m;
            }
            else{
                throw Error("Error: minute value must be >= 0 and < 60")
            }
        }

        time(){
            if(this.h.lenght != 2){
                if (this.h[0] == 0){
                    this.h = this.h - "0";
                }
                if (this.h < 10){
                this.h = "0" + this.h;
                }
            } 
            if (this.m < 10){
                this.m = "0" + this.m;
            }
            return(this.h + ":" + this.m)
        }

        deactivateAlarm(){
            this.alarmIsActive = false;
        }
        activateAlarm(){
            this.alarmIsActive = true;
        }

        tick(){
                this.m ++;
            if(this.m == 60){
                this.m = 0;
                this.h ++;
            }
        
            if(this.h == 24){
            this.h -= 24;
            }   

            if(this.h == this.h2 && this.m == this.m2){
                if (this.alarmIsActive == true){
                    console.log("Alarm!!!");
                }
            }
        }
        minuteticker() {
            minutvisare = this.m + 5;
        }
    }

    let klocka = new clock(4, 55)
    let klocka1 = new clock(5, 55)
    let klocka2 = new clock(6, 55)
    var minutvisare = ""
    let minutes = spring(
        parseInt(klocka2.h) * 60 + parseInt(klocka2.m)
    );
    function updateHour(){
        hourCounter = klocka2.h*10+10
    }

    setInterval(()=>{klocka.tick(); klocka = klocka;}, 1000)
    setInterval(()=>{klocka1.tick(); klocka1 = klocka1;}, 1000)
    setInterval(updateHour, 1000);
    setInterval(()=>{
        klocka2.tick(); 
        minutes.set(
            parseInt(klocka2.h) * 60 + parseInt(klocka2.m)
        );}
        , 1000)
        
        var hourCounter = "";
            
    let alarm = ""
    let alarm1 = ""
    let alarm2 = ""

    function setAlarm(){
        console.log(alarm)
    }

</script>

<main>
    <div class="grid-container">
        <div class="grid-item">
            <svg width="360" height="120">
                <rect width={hourCounter} height="120" style="fill:rgb(15, 56, 146);stroke-width:3;stroke:rgb(0,0,0)" />
            </svg>
            <svg width="360" height="120">
                <rect width={360*(($minutes%60)/60)} height="120" style="fill:rgb(15, 56, 146);stroke-width:3;stroke:rgb(0,0,0)" />
            </svg>
            <input type="time" id="alarm" bind:value={alarm}>
        
            <div class="row">
                <button on:click={()=>{klocka2.tick(); klocka2 = klocka2;}}
                    >tick</button
                >
            
                <button on:click={()=>{klocka2.tick(); klocka2 = klocka2;}}
                    >tick</button
                >
                </div>

            <label class="switch">
                <input type="checkbox">
                <span class="slider round"></span>
            </label>
        
            {#if klocka.time() == alarm}
            <script>
                alert("1");
            </script>
            {/if}
        </div>
        <div class="grid-item">
            <div class="wrapper">
                <div class="display">
                    <div id="time">{klocka1.time()}</div>
                </div>
            </div>
            <input type="time" id="alarm1" bind:value={alarm1}>
        
            <div class="row">
            <button on:click={()=>{klocka1.tick(); klocka1 = klocka1;}}
                >tick</button
            >
        
            <button on:click={()=>{klocka1.tick(); klocka1 = klocka1;}}
                >tick</button
            >
            </div>
        
            <label class="switch">
                <input type="checkbox">
                <span class="slider round"></span>
            </label>
        
            {#if klocka1.time() == alarm1}
            <script>
                alert("2");
            </script>
            {/if}
        </div>
        <div class="grid-item">
            <svg viewBox="-50 -50 100 100">
                <circle class="clock-face" r="48" />
            
                <!-- markers -->
                {#each [0, 5, 10, 15, 20, 25, 30, 35, 40, 45, 50, 55] as minute}
                    <line class="major" y1="40" y2="45" transform="rotate({30 * minute})" />
            
                    {#each [1, 2, 3, 4] as offset}
                        <line
                            class="minor"
                            y1="42"
                            y2="45"
                            transform="rotate({6 * (minute + offset)})"
                        />
                    {/each}
                {/each}
            
                <!-- hour hand -->
                <line
                    class="hour"
                    y1="33"
                    y2="38"
                    transform="rotate({(6 / 12) * $minutes - 180})"
                />
            
                <!-- minute hand -->
                <g transform="rotate({6 * $minutes - 180})">
                    <line class="minute" y1="30" y2="38" />
                </g>
            </svg>
            <input type="time" id="alarm2" bind:value={alarm2}>
        
            <div class="row">
            <button on:click={()=>{klocka2.tick(); klocka2 = klocka2;}}
                >tick</button
            >
        
            <button on:click={()=>{klocka2.tick(); klocka2 = klocka2;}}
                >tick</button
            >
            </div>
        
            <label class="switch">
                <input type="checkbox">
                <span class="slider round"></span>
            </label>
        
            {#if klocka2.time() == alarm2}
            <script>
                alert("3");
            </script>
            {/if}        
        </div>

</main>

<style>
    :global(body){
        background:  rgb(27, 27, 27);
    }
    
    main {
        color: white;
        display: grid;
        height: 100%; 
        place-items: center;
        font-family: 'Roboto Mono', monospace;
    }

    .grid-container {
  display: flex;
  padding: 50px;
  gap: 50px;
  border: rgb(39,97,116,1);
  
}
    .grid-item {
  background-color: rgb(27, 27, 27);
  display: flex;
  flex-direction: column;
  justify-items: center;
  align-items: center;
}

    .wrapper{
        height: 120px;
        width: 360px;
        background-image: linear-gradient(-200deg,
        rgb(120, 160, 245) 0%,
        rgb(39,97,116,1) 50%,
        rgb(21, 44, 59) 100%);
        border-radius: 10px;
        animation: animate 4s linear infinite;
        display: block;
    }
    @keyframes animate{
        100%{
            filter: hue-rotate(360deg);
        }
}
    .wrapper .display{
        box-sizing:border-box;
        margin: 20px;
        background:rgb(27, 27, 27);
        border-radius: 6px;
        max-width: 100%;
        max-height: 100%;
    }
    .wrapper .display #time{
        line-height: 85px;
        font-size: 50px;
        letter-spacing: 1px;
        text-align: center;
    }

    .switch {
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
  cursor: pointer;
  top: 0;
  left: 0;
  right: 0;
  bottom: 0;
  background-color: #ccc;
  -webkit-transition: .4s;
  transition: .4s;
}

.slider:before {
  content: "";
  height: 26px;
  width: 26px;
  left: 4px;
  bottom: 4px;
  background-color: white;
  -webkit-transition: .4s;
  transition: .4s;
}

input:checked + .slider {
  background-color: rgb(21, 44, 59);
}

input:checked + .slider:before {
  -webkit-transform: translateX(26px);
  -ms-transform: translateX(26px);
  transform: translateX(26px);
}

.slider.round {
  border-radius: 34px;
}

.slider.round:before {
  border-radius: 50%;
}

svg {
        width: 100%;
        height: 100%;
    }

    .clock-face {
        stroke: #333;
        fill: none;
    }

    .minor {
        stroke: rgb(56, 56, 56);
        stroke-width: 0.4;
    }

    .major {
        stroke: #333;
        stroke-width: 0.8;
    }

    .minute {
        stroke: rgb(180, 0, 0);
        stroke-width: 1;
    }

    .hour {
        stroke: #333;
        stroke-width: 2;
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
