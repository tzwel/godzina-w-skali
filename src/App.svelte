<script>

  const diviser = 4.1666666666666666666666666666667;

  let time = {}

  let converting = false
  let timeToConvert = Date.now();

  let converterHour, converterMinute, converterSecond;


  function calcTime() {

    if (converterHour || converterMinute || converterSecond) {
      timeToConvert = `2000-01-17T${pad(converterHour.value)}:${pad(converterMinute.value)}:${pad(converterSecond.value)}`
    } else {
      timeToConvert = Date.now();
    }

    time.date = new Date(timeToConvert);
    time.nowString = time.date.getHours() + ':' + pad(time.date.getMinutes()) + ':' + pad(time.date.getSeconds());
    time.nowPercents = (Number('' + pad(time.date.getHours()) + pad(time.date.getMinutes()) + pad(time.date.getSeconds())) / 10000) * diviser;
    time.nowInScale = time.nowPercents / 10
  }

  calcTime()
  

  function pad(n) {return ("0" + n).slice(-2)}

  setInterval(calcTime, 1000)

</script>

<main>

  <button class="floating" on:click={()=>{converting = !converting}}> Konwertuj </button>

  <h2> {converting ? 'Konwertujesz' : 'Teraz jest'} </h2>
  
  {#if converting}
    <div class="converterInputs">
      <input on:change={calcTime} bind:this={converterHour} min="0" max="23" type="number" value={pad(new Date().getHours())} placeholder={pad(new Date().getHours())}> <span> : </span>
      <input on:change={calcTime} bind:this={converterMinute} min="0" max="59" type="number" value={pad(new Date().getMinutes())} placeholder={pad(new Date().getMinutes())}> <span> : </span>
      <input on:change={calcTime} bind:this={converterSecond} min='0' max="59" type="number" value={pad(new Date().getSeconds())} placeholder={pad(new Date().getSeconds())}>
    </div>
  {:else}
    <h1 class="hour big"> {time.nowString} </h1>
  {/if}

  <section class="grid">
    <div class="panel">
      <h3> Godzina od 0 do 100%</h3>
      <span class="hour">
        {time.nowPercents.toPrecision(3)}
      </span> <strong class="scale">/100%</strong>
    </div>
  
    <div class="panel">
      <h3> Godzina w skali od 0 do 10 </h3>
      <span class="hour">
        {time.nowInScale.toPrecision(2)}
      </span> <strong class="scale">/10</strong>
    </div>
  </section>

</main>

<style>

  .converterInputs {
    margin-top: 1rem;
  }

  input {
    min-width: 2ch;
    width: calc(2ch + 1rem + 4px);
    padding: 0.5rem;
    font-size: 3rem;
    font-weight: 700;

    border: none;
  background: #3a3a3a;
  border-radius: 4px;
  cursor: pointer;
  font-weight: 700;
  font-family: inherit;
    
  }

  .scale {
    font-size: 1.5rem;
  }

  h2 {
    margin-bottom: 0;
    padding: 0;
  }

  h1, h3 {
    margin-top: .5rem;
  }

  h3 {
    margin-bottom: .33rem;
  }

  .hour {
    font-size: 2rem;
    font-weight: 700;
    color: #ede888;
  }

  h3 {
    font-size: 1rem;
    font-weight: 500;
  }

  .grid {
    display: flex;
  }

  .big {
    font-size: 3rem;
  }


  .panel {
    padding: 1rem;
  }

  .floating {
    position: absolute;
    top:0;
    right: 0;
    margin: 1rem;
    padding: .5rem .8rem;
  }

</style>
