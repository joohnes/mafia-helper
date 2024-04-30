<script lang="ts">
    function sendData() {
        // @ts-ignore
        var data = document.getElementById("players")?.value
        let names: string[] = data.toString().split(" ")
        let newUrl: string = window.location.href + "game?pnames=" + names.join(",")
        window.location.href = newUrl
    }
</script>

<form class="formGrid">
    <input class="css-input" style="width:100%; margin-top: 1rem;" id="players" type="text" placeholder="Type player names separated by space"/>
    <button class="btn" on:click={sendData}>Play</button>
</form>

<style>
    .formGrid {
        display: grid;
        width: 90%;
        margin: 0 auto;
        justify-items: center;
        gap: 2rem;
    }

    .css-input {
     padding: 8px;
     font-size: 16px;
     border-width: 1px;
     border-color: #CCCCCC;
     background-color: #FFFFFF;
     color: #000000;
     border-style: solid;
     border-radius: 10px;
     box-shadow: 0px 0px 5px rgba(66,66,66,.75);
     text-shadow: -2px 0px 5px rgba(66,66,66,.0);
     font-family: Montserrat,-apple-system,BlinkMacSystemFont,"Segoe UI",Helvetica,Arial,sans-serif,"Apple Color Emoji","Segoe UI Emoji","Segoe UI Symbol";
}
 .css-input:focus {
     outline:none;
}

.btn {
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
  min-width: 200px;
  outline: none;
  padding: 16px 24px;
  text-align: center;
  text-decoration: none;
  transition: all 300ms cubic-bezier(.23, 1, 0.32, 1);
  user-select: none;
  -webkit-user-select: none;
  touch-action: manipulation;
  will-change: transform;
}

.btn:disabled {
  pointer-events: none;
}

.btn:hover {
  /* color: #fff; */
  /* background-color: #1A1A1A; */
  box-shadow: rgba(0, 0, 0, 0.25) 0 8px 15px;
  transform: translateY(-2px);
}

.btn:active {
  box-shadow: none;
  transform: translateY(0);
}
</style>