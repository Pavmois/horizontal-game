<template>
  <div class="hello">
    <h1>{{ msg }}</h1>

    <div class='roulette-wrapper'>
      <div class='selector'></div>
      <div class='wheel'>
        <div class="row">
          <div class="card" v-for="item in roulette_items" :key="item.id">{{ item }}</div>
        </div>
      </div>
    </div>

    <div>
      <input type="number" v-model="inputValue" placeholder='Введи от 1 до 10'>
      <button v-on:click="spin" v-show="btnShow1">Старт</button>
      <button v-on:click="stopSpin" v-show="btnShow2">Старт</button>
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
    btnShow1: true,
    btnShow2: false
  }),
  methods: {
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
      this.base.sort(() => Math.random() - 0.5);
    },
    // Остановка рулетки и сброс позиции
    stopSpin: function() {
      this.btnShow2 = !this.btnShow2;
      this.btnShow1 = !this.btnShow1;

      let content = document.querySelector(".wheel");
      content.style.setProperty('transition-timing-function','');
      content.style.setProperty('transition-duration','');
      content.style.setProperty('transform', 'translate3d(0px, 0px, 0px)');

    },
    // Запуск рулетки
    spin: function() {
      this.btnShow1 = !this.btnShow1;
      this.btnShow2 = !this.btnShow2;

      let content = document.querySelector(".wheel"),
  		order = this.base,
      position = order.indexOf(Number(this.inputValue));

      // Определение конечной позиции
      let card = 75 + 4 * 2,
          landingPosition = (order.length * card) + (position * card);
      let randomize = Math.floor(Math.random() * 75) - (75/2);
      landingPosition = landingPosition + randomize;
      let object = {
        x: Math.floor(Math.random() * 50) / 100,
        y: Math.floor(Math.random() * 20) / 100
      };

      // Анимация
      content.style.setProperty(
        'transition-duration',''+this.rotation_duration+'ms'
      );
      content.style.setProperty(
        'transform','translate3d(-'+landingPosition+'px, 0px, 0px)'
      );
      content.style.setProperty(
        'transition-timing-function','cubic-bezier(0,'+ object.x +','+ object.y + ',1)'
      );
    },
  },
  beforeMount() {
    this.baseCreate();
    this.arrayShuffle();
    this.arrayCreate();
  }
}
</script>


<style scoped>
.roulette-wrapper{
  position:relative;
  display:flex;
  justify-content:center;
  width:80%;
  height: 80px;
  margin:20px auto;
  overflow:hidden;
  border: 2px solid rgb(225, 0, 255);
  border-radius: 8px;
}

.roulette-wrapper .selector{
  width:4px;
  height:100%;
  background:rgb(207, 5, 5);
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

button {
  cursor: pointer;
}

h3 {
  margin: 40px 0 0;
  text-align: center;
}
</style>
