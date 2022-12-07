<template>
  <div class="calculator" id="app">
    <div class="calculator__screen">
      {{ line }}
    </div>
    <div class="calculator__buttons">
      <span @click="clear" class='b-clear'>clear</span>
      <span v-for="button in buttons" @click="buildExpression" :key="button">
        {{ button }}
      </span>
      <span @click="calculate" class="b-calc">=</span>
    </div>
  </div>
</template>

<script>
 export default {
  name: 'App',
  data() {
    return {
      buttons: ['*',1,2,3,':',4,5,6,'+',7,8,9,'-',0],
      line: 0,
      name: "Vue.js"
    };
  },
  methods: {
    clear () {
      this.line = "";
    },
    calculate() {
      this.line = eval(this.line.replace(":","/"));
    },
    buildExpression(event) {
      if (event) {
        if (this.line == 0) this.line = "";
        
        if ( (['*',":","+","-"].includes(event.target.innerHTML)) && (['*',":","+","-"].includes(this.line[this.line.length-1])) )  {
          this.line[this.line.length-1] = event.target.innerHTML
        } else
        this.line += event.target.innerHTML;
      }
    }
  }
}
</script>

<style lang="scss">
$background: #5cdb95;
$white: #edf5e1;
$tablo: #05386b;
$grey: #dfe7d2;
$accent: #379683;

.calculator {
  background-color: $white;
  max-width: 420px;
  display: block;
  margin: 50px auto;
  padding: 2em;
  border-radius: 10px;
  border: 1px solid $grey;
  line-height: 1;
  -webkit-box-shadow: 0px 5px 10px 2px rgba(34, 60, 80, 0.2);
  -moz-box-shadow: 0px 5px 10px 2px rgba(34, 60, 80, 0.2);
  box-shadow: 0px 5px 10px 2px rgba(34, 60, 80, 0.2);


  &__screen {
    height: 26px;
    background-color: $tablo;
    color: $white;
    padding: 1em;
    margin-bottom: 10px;
    font-size:1.6em;
  }

  &__buttons {
    display: grid;
    grid-gap: 10px;
    grid-template-columns: repeat(4, [col] auto);
    grid-template-rows: repeat(5, [row] auto);
    background-color: $white;
    color: $tablo;

    span {
      padding: 1em;
      text-align: center;
      background-color: $grey;
      font-weight: 500;
      font-size: 1.3rem;
      border-radius: 20px;
      -webkit-box-shadow: -5px -5px 5px -5px rgba(34, 60, 80, 0.6) inset;
      -moz-box-shadow: -5px -5px 5px -5px rgba(34, 60, 80, 0.6) inset;
      box-shadow: -5px -5px 5px -5px rgba(34, 60, 80, 0.6) inset;
      transition: all 0.5s;
      cursor: pointer;
      &:hover {
        background-color: $accent;
        
        color: $white;
      }
    }

    .b-clear {
      grid-column: col / span 3;
      grid-row: row 1;
    }
    .b-calc {
      grid-column: col 2 / span 3;
      grid-row: row 5;
      background-color: $accent;
      color: $white;
    }
  }
}
</style>
