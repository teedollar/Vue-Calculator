<template>
  <div class="calculator container">
     <div class="row">
        <div class="display col-12"> {{ current }} </div>
         <div class="display equalToDisplay col-12"> {{ equalToDisplay }} </div>
         <div class="btn col-3" @click="clear"> C </div>
         <div class="btn col-3" @click="sign"> +/- </div>
         <div class="btn col-3" @click="percent"> % </div>
         <div class="btn operator col-3" @click="divide"> / </div>
         <div class="btn col-3" @click="append('7')"> 7 </div>
         <div class="btn col-3" @click="append('8')"> 8 </div>
         <div class="btn col-3" @click="append('9')"> 9 </div>
         <div class="btn operator col-3" @click="times"> x </div>
         <div class="btn col-3" @click="append('4')"> 4 </div>
         <div class="btn col-3" @click="append('5')"> 5 </div>
         <div class="btn col-3" @click="append('6')"> 6 </div>
         <div class="btn operator col-3" @click="minus"> - </div>
         <div class="btn col-3" @click="append('1')"> 1 </div>
         <div class="btn col-3" @click="append('2')"> 2 </div>
         <div class="btn col-3" @click="append('3')"> 3 </div>
         <div class="btn operator col-3" @click="add"> + </div>
         <div class="btn col-3" @click="appendZero"> 0 </div>
         <div class="btn dot col-3" @click="dot"> . </div>
         <div class="btn col-3" @click="del"> del. </div>
         <div class="btn operator col-3" @click="equal"> = </div>
     </div>

  </div>
</template>

<script>
export default {
  data() {
    return {
      stringPressed: null,
      previous: null,
      current: '',
      equalToDisplay: '',
      operator: null,
      operatorClicked: null,
    }
  }, 

  methods: {
    clear() {
      this.curret = null,
      this.current = '';
      this.equalToDisplay = '';
    },

    del() {
      this.current = this.current.slice(0, -1);
    },

    sign() {
      this.current = this.current.charAt(0) === '-' ? this.current.slice(1) : `-${this.current}`;
    },

    percent() {
    this.current = `${parseFloat(this.current) / 100}`
    },

    append(number) {
      if(this.operatorClicked){
        this.current = '';
        this.operatorClicked = false;
      }
      if( (this.current.length > 0) && (this.current.charAt(0) == '0') && (this.current.charAt(1) != '.') ) {
        this.current = this.current.slice(1);
      }
      this.current = `${this.current}${number}`;
    },

    appendZero() {
      if(this.current != '0' ) {
        this.append('0')
      }
      
    },

    dot() {
      if(this.current.indexOf('.') === -1) {
        this.append('.');
        if(this.current == '.'){
          this.current = '0.';
        }
      }
      
      
    },

    setPrevious() {
      this.previous = this.current;
      this.operatorClicked = true;
    },

    divide() {
      this.operator = (a, b) => a / b;
      this.setPrevious();
    },

    times() {
      this.operator = (a, b) => a * b;
      this.setPrevious();
    },

    minus() {
      this.operator = (a, b) => a - b;
      this.setPrevious();
    },

    add() {
      this.operator = (a, b) => a + b;
      this.setPrevious();
    },

    equal() {
      this.equalToDisplay = `${this.operator(
        parseFloat(this.previous), 
        parseFloat(this.current)
      )}`;
      this.previous = this.equalToDisplay;
    }
  }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>

.calculator {
  width: 400px;
  margin: 0 auto;
  font-size: 40px;
  
}

.display {
  
  background-color: #333;
  color: #ffffff;
  height: 60px;
  text-align: right;
  padding-top: 16px;
  padding-right: 10px;
  vertical-align: middle;
  
}


.equalToDisplay {
  color: orange;
  font-size: 30px;
  padding-buttom: 25px;

}

.zero {
  grid-column: 1 / 3;
  
}

.btn {
  background-color: #F2F2F2;
  border: 1px solid #999;
  pointer: cursor;
}

.dot {
 text-align: center;
 vertical-align: middle;

}

.operator {
  background-color: orange;
  color: #ffffff;
}

</style>
