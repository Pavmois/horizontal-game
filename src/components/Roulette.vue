<template>
  <div class="hello">
    <h1>{{ msg }}</h1>

    <div class='roulette-wrapper'>
      <div class='selector'></div>
      <div class='wheel'>
        <div class="row">
          <div class="card">1</div>
          <div class="card">2</div>
          <div class="card">3</div>
          <div class="card">4</div>
          <div class="card">5</div>
          <div class="card">6</div>
          <div class="card">7</div>
          <div class="card">8</div>
          <div class="card">9</div>
          <div class="card">10</div>
          <div class="card">1</div>
        </div>
      </div>
    </div>

    <div>
      <input placeholder='Введи от 1 до 10'>
      <button>Старт</button>
    </div>

    <h3>
      Правила просты:<br>
      <br>
      Вводишь число - Жмёшь кнопку "Старт" - Побеждаешь!
    </h3>
  </div>
</template>

<script>
export default {
  name: 'Roulette',
  props: {
    msg: String
  }
}
</script>


<style scoped>
.roulette-wrapper{
  position:relative;
  display:flex;
  justify-content:center;
  width:40%;
  height: 80px;
  margin:20px auto;
  overflow:hidden;
  border: 1px solid red;
}

.roulette-wrapper .selector{
  width:4px;
  height:100%;
  background:rgb(0, 255, 76);
  left:50%;
  transform:translate(-50%,0%);
  position:absolute;
  z-index:2;
}

.roulette-wrapper .wheel{
  display:flex;
}

.roulette-wrapper .wheel .row{
  display:flex;
}

.roulette-wrapper .wheel .row .card{
  height:70px;
  width:70px;
  margin:4px;
  border-radius:8px;
  display:flex;
  align-items:center;
  justify-content:center;
  color:white;
  font-size:1.5em;
  border: 1px solid yellow;
  background: rgba(0, 0, 0, 0.541);
}

h3 {
  margin: 40px 0 0;
  text-align: center;
}
</style>
