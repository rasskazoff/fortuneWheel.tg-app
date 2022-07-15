<template>
  <div class="wheel_wrap">
    <h1>Жми на колесо</h1>
    <Wheel
      ref="wheel"
      :gift="gift"
      :data="data"
      @done="done"
      :imgParams="logo"
      @click="spinTheWheel"
    />
  </div>

</template>

<script>
let tg = window.Telegram.WebApp; //получаем объект webapp телеграма 

tg.expand(); //расширяем на все окно
tg.MainButton.setParams({"text":"Забрать подарок","color": "#007730","textColor":"#ffffff" });

import { Wheel } from "vue3-fortune-wheel";
//import 'vue3-fortune-wheel/dist/library.css'

export default {
  name: "App",
  components: {
    Wheel,
  },
  data() {
    return {
      gift: Math.floor(Math.random() * 6),
      logo: {
        width: 100,
        height: 120,
        src:
          "https://papik.pro/uploads/posts/2022-01/1642418311_27-papik-pro-p-stikeri-pepe-30.png",
      },
      data: [
        {
          id: 1,
          value: "Приз 1",
          bgColor: "#007730",
          color: "#ffffff",
        },
        {
          id: 2,
          value: "Приз 2",
          bgColor: "#ffffff",
          color: "#000000",
        },
        {
          id: 3,
          value: "Приз 3",
          bgColor: "#c92729",
          color: "#ffffff",
        },
        {
          id: 4,
          value: "Приз 4",
          bgColor: "#007633",
          color: "#ffffff",
        },
        {
          id: 5,
          value: "Приз 5",
          bgColor: "#ffffff",
          color: "#000000",
        },
        {
          id: 6,
          value: "Приз 6",
          bgColor: "#c92729",
          color: "#ffffff"
        },
      ],
    };
  },
  methods: {
    done(params) {
      console.log(params.value);
      tg.MainButton.show();
      tg.onEvent('mainButtonClicked', function(){
        tg.sendData('Ваш приз: '+params.value); 
        //при клике на основную кнопку отправляем данные в строковом виде
      });
    },
    spinTheWheel() {
      this.$refs.wheel.spin();
    },
  },
};

</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 30px;
}
.wheel_wrap {
  display: flex;
  flex-direction: column;
  justify-content: center;
  align-items: center;
}
</style>
