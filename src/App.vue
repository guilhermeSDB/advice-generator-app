<template>
  <div class="container">
    <h1 class="title">Advice #{{id}}</h1><!-- Advice ID goes here -->
    <MessageVue :message="dados" />
    <picture class="entalhe">
      <source media="(max-width: 425px)" srcset="@/assets/pattern-divider-mobile.svg" />
      <img src="@/assets/pattern-divider-desktop.svg" alt="" />
    </picture>
    <button class="btnGerar" @click="getRandomAdvice"><img src="@/assets/icon-dice.svg" alt=""></button>
  </div>
</template>

<script>
import MessageVue from './components/Message.vue';
export default {
  name: 'App',
  components: {
    MessageVue
  },
  data (){
    return{
      dados: null,
      id: null,
    }
  },
  methods:{
    async getRandomAdvice(){
      let spinnerElement = document.querySelector(".spinner").classList;
      let messageElement = document.querySelector(".message").classList;

      messageElement.add("d-none");
      spinnerElement.remove("d-none");
      
      const response = await fetch("https://api.adviceslip.com/advice");
      const data = await response.json();
      this.dados = data.slip.advice;
      this.id = data.slip.id;

      messageElement.remove("d-none");
      spinnerElement.add("d-none");
    }
  },
  mounted(){
      this.getRandomAdvice()
  }
  
}
</script>

<style lang="scss">
@import url('https://fonts.googleapis.com/css2?family=Manrope:wght@200;300;400;500;600;700;800&display=swap');

:root{
  --LightCyan: hsl(193, 38%, 86%);
  --NeonGreen: hsl(150, 100%, 66%);
  --GrayishBlue:  hsl(217, 19%, 38%);
  --DarkGrayishBlue: hsl(217, 19%, 24%);
  --DarkBlue: hsl(218, 23%, 16%);
}

*{
  margin: 0;
  padding: 0;
  box-sizing: border-box;
  
}

#app {
  width: 100vw;
  min-height: 100vh;
  font-family: 'Manrope', sans-serif;
  font-weight: 800;
  color:var(--LightCyan);
  background-color: var(--DarkBlue);

  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;

  display: flex;
  justify-content: center;
  align-items: center;

  .container{
    display: flex;
    flex-direction: column;
    width: 30rem;
    text-align: center;
    border-radius: 15px;
    background-color:var(--DarkGrayishBlue);
    padding: 24px;
    position: relative;
    transition: height 0.4s;

    @media (max-width: 450px){ margin: 1rem; }

    .title{
      text-transform: uppercase;
      font-size: 12px;
      color:var(--NeonGreen);
      letter-spacing: 6px;
      margin: 16px 0;

      @media (max-width: 450px){ font-size: 10px; }

    }

    .entalhe{
      width: 100%;
      margin: 2rem 0;

      @media (max-width: 450px){ margin: 1rem 0 2rem 0; }

      img{
          width: 100%;
      }
    }

    .btnGerar{
      width:4.2rem;
      height: 4.2rem;

      display: flex;
      justify-content: center;
      align-items: center;

      position: absolute;
      bottom: -2rem;
      border-radius: 250px;
      border: none;
      background-color:var(--NeonGreen);
      align-self: center;
      cursor: pointer;
      transition: 0.4s;

      @media (max-width: 450px){ width: 3.8rem; height: 3.8rem;}

      &:hover{
        box-shadow: 0px 0px 20px 4px #52ffa8;
        -webkit-box-shadow: 0px 0px 20px 4px #52FFA8; 
      }

    }
  }

}

</style>
