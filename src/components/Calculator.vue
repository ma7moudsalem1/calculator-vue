<template>
  <div class="calculator">
      <div class="result">
        <small class="screen-operator" v-show="operationCheck()">{{previous}} {{operator}}</small>
        {{ result || '0' }}
        </div>
      <div @click="clear" class="btn">C</div>
      <div @click="sign" class="btn">+/-</div>
      <div @click="percent" class="btn">%</div>
      <div @click="setOperator('/')" class="btn operator">/</div>
      <div @click="append(7)" class="btn">7</div>
      <div @click="append(8)" class="btn">8</div>
      <div @click="append(9)" class="btn">9</div>
      <div @click="setOperator('*')" class="btn operator">x</div>
      <div @click="append(4)" class="btn">4</div>
      <div @click="append(5)" class="btn">5</div>
      <div @click="append(6)" class="btn">6</div>
      <div @click="setOperator('-')" class="btn operator">-</div>
      <div @click="append(1)" class="btn">1</div>
      <div @click="append(2)" class="btn">2</div>
      <div @click="append(3)" class="btn">3</div>
      <div @click="setOperator('+')" class="btn operator">+</div>
      <div @click="append(0)" class="zero btn">0</div>
      <div @click="dot" class="btn">.</div>
      <div @click="equal" class="btn operator">=</div>
  </div>
</template>

<script>
export default {
  data(){
    return {
      result: '',
      previous: null,
      operatorClicked: false,
      operator: null
    }
  },
  methods: {
    clear(){
      this.result = '';
      this.setToDefault();
    },

    sign(){
      this.result = this.result == 0 ? this.result : (String(this.result).charAt(0) == '-' ? String(this.result).slice(1) : `-${this.result}`);
    },

    percent(){
      this.result = `${parseFloat(this.result)}` / 100;
    },

    append(number){
      this.result = this.result == '0' ? `${number}` : `${this.result}${number}`;
    },

    dot(){
      if(this.result.indexOf('.') === -1){
        this.append('.');
      }
    },

    operationCheck(){
      return this.operatorClicked && this.operator != null ? true : false;
    },

    setOperator(operator){
      if(this.operationCheck()){
        this.equal();
      }
      this.previous        = this.result;
      this.operatorClicked = true;
      this.operator        = operator;
      this.result          = ''
    },

    setToDefault(){
      this.previous        = null;
      this.operatorClicked = false;
      this.operator = null;
    },

    equal(){
      if(this.operationCheck()){
        switch(this.operator){
          case '+':
            this.result = parseFloat(this.result) + parseFloat(this.previous);
            break; 
          case '-':
            this.result =  parseFloat(this.previous) - parseFloat(this.result);
            break;
          case '/':
            this.result = parseFloat(this.previous) / parseFloat(this.result);
            break;
          case '*':
            this.result = parseFloat(this.result) * parseFloat(this.previous);
            break; 
        }
        this.setToDefault();
      }
    }
    
  }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
  .calculator{
    width: 400px;
    margin: 20px auto;
    display: grid;
    grid-template-columns: repeat(4, 1fr);
    grid-auto-rows: minmax(50px, auto);
  }
  .result{
    font-size: 40px;
    grid-column: 1/5;
    background: #333;
    color: #FFF;
  }
  .zero{
    grid-column: 1/3;
  }
  .btn{
    background-color: #f2f2f2;
    border: .5px solid #333;
    padding: 15px;
    cursor: pointer;
  }
  .operator{
    background-color: orange;
    color: #FFF;
  }
  .screen-operator{
    color: red;
    font-size: 50%
  }
</style>
