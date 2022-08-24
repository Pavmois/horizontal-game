<template>
  <div class="hello">
    <h1>{{ msg }}</h1>

    <div class='roulette-wrapper'>
      <div class='selector'></div>
      <div class='wheel'>
        <div class="row">
          <div class="card" v-for="item in base" :key="item.id">{{item}}</div>
        </div>
      </div>
    </div>

    <div>
      <input type="number" v-model="inputValue" placeholder='Введи от 1 до 10' id="inputField">
      <button v-on:click="spin">Старт</button>
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
  },
  data: () => ({
    base: [],
    roulette_items_amount: 200,
    rotation_duration: 10000,
    roulette_items: [],
    baseNum: 10,
    inputValue: NaN,
    buttonDisable: false
  }),
  methods: {
    // Запуск рулетки
    spin: function() {
      //this.inputValue = Number(this.inputValue);

    },
    // Функция для автоматического изменения Base на случай если нужно будет делать другой интервал значений
    baseCreate: function() {
      this.base = [...Array(this.baseNum+1).keys()].slice(1);
    },
    // Функция для автоматической генерации массива с максимальным количеством слотов
    arrayCreate: function() {
      for (let i = this.roulette_items.length; this.roulette_items.length != this.roulette_items_amount; i++ ) {
        this.roulette_items = this.roulette_items.concat(this.base);
      }
    },
    // Функция для перемешивания массива
    arrayShuffle: function() {
      this.roulette_items.sort(() => Math.random() - 0.5);
    }
  },
  beforeMount() {
    this.baseCreate();
    this.arrayCreate();
    this.arrayShuffle();
    this.inputValue = Number(this.inputValue);
  },
  // watch: {
  //   'inputValue'(value) {
  //     console.log(value);
  //   }
  // }
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
  /* animation: fadeleft 2s ease infinite alternate; */
}
@keyframes fadeleft {
  0% {
     transform: translateX(0);
  }
  100% {
     transform: translateX(-20%);
  }
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
