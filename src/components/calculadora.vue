<template>
  <div class="calculadora">
    <div class="display">{{ valorCorrente || '0'}}</div>
    <div class="botao">CE</div>
    <div v-on:click="limpar" class="botao">C</div>
    <div v-on:click="porc" class="botao">%</div>
    <div v-on:click="div" class="botao">÷</div>
    <div v-on:click="concnum(7)"  class="botaon">7</div>
    <div v-on:click="concnum (8)"  class="botaon">8</div>
    <div v-on:click="concnum(9)"  class="botaon">9</div>
    <div v-on:click="mult" class="botao">x</div>
    <div v-on:click="concnum(4)" class="botaon">4</div>
    <div v-on:click="concnum(5)" class="botaon">5</div>
    <div v-on:click="concnum(6)" class="botaon">6</div>
    <div v-on:click="sub" class="botao">-</div>
    <div v-on:click="concnum(1)" class="botaon">1</div>
    <div v-on:click="concnum(2)" class="botaon">2</div>
    <div v-on:click="concnum(3)" class="botaon">3</div>
    <div v-on:click="soma" class="botao">+</div>
    <div v-on:click="sinal" class="botaon">±</div>
    <div v-on:click="concnum(0)" class="botaon">0</div>
    <div v-on:click="ponto"  class="botaon">.</div>
    <div v-on:click="result" class="botaoi">=</div>

  </div>
</template>

<script>
export default {
  data(){
    return{ 
      valorCorrente: '',
      numant: null,
      ope: null,
      opesel: false 
    };
  },
    methods: {

      limpar() {
        this.valorCorrente = '' ;       
      },
      sinal(){ 
        this.valorCorrente = this.valorCorrente.charAt(0) === '-'
          ? this.valorCorrente.slice(1)
          :`-${this.valorCorrente}`;
      },
      porc(){
        this.valorCorrente = `${parseFloat(this.valorCorrente) / 100}`;
      },
      concnum(num){
        if (this.opesel) {
          this.valorCorrente = '';
          this.opesel = false;
        }
        this.valorCorrente = `${this.valorCorrente}${num}`;
      },
      ponto(){
        if (this.valorCorrente.indexOf('.') === -1){
          this.concnum('.');
        }
      },
      setnum(){
        this.numant = this.valorCorrente;
        this.opesel = true; 
      },
      soma(){
        this.ope = (num1,num2)=> num1 + num2;
        this.setnum();
      },

      div(){
        this.ope = (num1,num2)=> num1 / num2;
        this.setnum();
      },

      mult(){
        this.ope = (num1,num2)=> num1 * num2;
        this.setnum();
      },
      sub(){
        this.ope = (num1,num2)=> num1 - num2;
        this.setnum();
      },
      result(){
        this.valorCorrente = `${this.ope(
          parseFloat(this.numant),
          parseFloat(this.valorCorrente),
        )}`;
        this.numant = null;
      },
    },
  };

</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>

.calculadora{
  margin: 0 auto;
  width: 700px;
  display: grid;
  font-size: 40px;
  grid-template-columns: repeat(4, 1fr);
  grid-auto-rows: minmax(50px, auto);
}
.display{
  grid-column: 1 / 5;
  background-color: rgb(62, 62, 63);
  color: white;
}
.botaon{
  background-color: rgb(233, 233, 233);
  border: 1px solid black;
}
.botao{
  background-color: rgb(170, 170, 170);
  border: 1px solid black;
}
.botaoi{
  background-color: rgb(255, 145, 0) ;
  border: 1px solid black;
}


</style>
