<script>

  const diviser = 4.1666666666666666666666666666667;

  let time = {}

  function calcTime() {
    time.unix = Date.now();
    time.date = new Date();
    time.nowString = time.date.getHours() + ':' + pad(time.date.getMinutes()) + ':' + pad(time.date.getSeconds());
    time.nowPercents = (Number('' + pad(time.date.getHours()) + pad(time.date.getMinutes()) + pad(time.date.getSeconds())) / 10000) * diviser;
    time.nowInScale = time.nowPercents / 10
  }

  calcTime()

  function pad(n) { return ("0" + n).slice(-2) }

  setInterval(calcTime, 1000)

</script>

<main>

  <h2> Teraz jest </h2>
  <h1 class="hour big"> {time.nowString} </h1>

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

</style>
