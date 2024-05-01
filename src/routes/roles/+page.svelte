<script lang="ts">
    import { page } from '$app/stores'
    
    const data = $page.url.searchParams.getAll("pnames")
    let names: string[] = data[0].split(",")
    var State = 0
    var Players: string[] = []

    function changeState(state: number) {
        State = state
        if (State == 6) {
            for (var i = 0; i < names.length; i++) {
                    document.getElementById(names[i])?.classList.remove("katani", "dead", "asasyn", "mafia", "medyk")
                }
        }
    }

    function startGame() {
        names.forEach(name => {
            if (document.getElementById(name)?.classList.contains("mafia")) {
                Players?.push(name+":"+"mafia")
            } else if (document.getElementById(name)?.classList.contains("katani")) {
                Players?.push(name+":"+"katani")
            } else if (document.getElementById(name)?.classList.contains("medyk")) {
                Players?.push(name+":"+"medyk")
            } else if (document.getElementById(name)?.classList.contains("asasyn")) {
                Players?.push(name+":"+"asasyn")
            } else {
                Players?.push(name+":"+"noname")
            }
        });
        // @ts-ignore
        console.log(Players)
        let newUrl: string = window.location.origin + "/game?pnames=" + Players.join(",")
        window.location.href = newUrl
    }

    function toggleRole(id: string) {
        switch (State) {
            case 1:
                document.getElementById(id)?.classList.toggle("mafia")
                break
            case 2:
                document.getElementById(id)?.classList.toggle("katani")
                break
            case 3:
                document.getElementById(id)?.classList.toggle("medyk")
                break
            case 4:
                document.getElementById(id)?.classList.toggle("asasyn")
                break
        }
    }


</script>

<div class="container">
    <div class="buttons">
        <button on:click={()=> {changeState(1)}} class="rolebtn mafia">Mafia</button>
        <button on:click={()=> {changeState(2)}} class="rolebtn katani">Katani</button>
        <button on:click={()=> {changeState(3)}} class="rolebtn medyk">Medyk</button>
        <button on:click={()=> {changeState(4)}} class="rolebtn asasyn">Asasyn</button>
        <button on:click={()=> {startGame()}} class="rolebtn">Start</button>
    </div>
    <div class="divider"/>
    <div class="buttons">
        {#each names as name}
            <!-- svelte-ignore a11y-click-events-have-key-events -->
            <!-- svelte-ignore a11y-no-static-element-interactions -->
            <div id={name} 
            class="playerCard rolebtn"
            on:click={()=>{toggleRole(name)}}
            >
                <span class="playerName">{name}</span>
            </div>
        {/each}
    </div>
</div>

<style>
    @import url('https://fonts.googleapis.com/css?family=Montserrat');

    .container {
        margin: 0 auto; 
        width: 100%; 
    }
    @media only screen and  (min-width: 851px) {
        .container {
            display: flex; 
            flex-direction: column; 
            align-items: center;
        }
    }

    .divider {
        margin: 1rem;
        background-color: black;
        height: 1px;
        width: 100%;
    }
.rolebtn {
  appearance: none;
  background-color: #ededed;
  border: 2px solid #1A1A1A;
  border-radius: 15px;
  box-sizing: border-box;
  color: #3B3B3B;
  cursor: pointer;
  display: inline-block;
  font-family: Montserrat,-apple-system,BlinkMacSystemFont,"Segoe UI",Helvetica,Arial,sans-serif,"Apple Color Emoji","Segoe UI Emoji","Segoe UI Symbol";
  font-size: 16px;
  font-weight: 600;
  line-height: normal;
  margin: 0;
  min-height: 60px;
  outline: none;
  padding: 16px 24px;
  text-align: center;
  text-decoration: none;
  transition: all 300ms cubic-bezier(.23, 1, 0.32, 1);
  user-select: none;
  -webkit-user-select: none;
  touch-action: manipulation;
  width: 100%;
  will-change: transform;
}

@media only screen and (max-width: 850px) {
    .rolebtn {
        min-width: 11rem!important;
    }
}

.rolebtn:disabled {
  pointer-events: none;
}

.rolebtn:hover {
  /* color: #fff; */
  /* background-color: #1A1A1A; */
  box-shadow: rgba(0, 0, 0, 0.25) 0 8px 15px;
  transform: translateY(-2px);
}

.rolebtn:active {
  box-shadow: none;
  transform: translateY(0);
}
    .buttons {
        width: 60%;
        display: grid;
        grid-template-columns: 1fr 1fr;
        gap: 10px;
        margin-bottom: 20px;
    }

    .playerName {
        display: table;
        margin: 0 auto;
    }

    :global(.mafia) {
        background-color: rgb(224, 0, 0)!important;
        color: #fff!important;
    }
    :global(.medyk) {
        background-color: blueviolet!important;
        color: #fff!important;
    }
    :global(.katani) {
        background-color: rgb(70, 70, 255)!important;
        color: #fff!important;
    }
    :global(.asasyn) {
        background-color: aqua!important;
    }
    :global(.dead) {
        background-color: #1A1A1A!important;
        color: #fff!important;
    }
    :global(.kCheck) {
        border-color: red!important;
    }
</style>