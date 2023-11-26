<template>
  <div class="container p-3 mt-3 rounded bg-warning">
    <p class="text-center fs-3 fw-bold p-2 text-primary">Számológép</p>
  </div>

 <div class="container mt-4">
  <div class="calculator">
    <div class="display text-end p-3 fw-bold rounded bg-secondary">{{current || '0'}}</div>
    <div @click="clear" class="btn fw-bold fs-2 text-center">C</div>
    <div @click="sign" class="btn fw-bold fs-2 text-center">+/-</div>
    <div @click="square" class="btn fw-bold fs-2 text-center">X<sup>2</sup></div>
    <div @click="divide" class="btn operator bg-danger fs-2 text-center p-1">÷</div>
    <div @click="append('7')" class="btn fw-bold fs-2 text-center">7</div>
    <div @click="append('8')" class="btn fw-bold fs-2 text-center">8</div>
    <div @click="append('9')" class="btn fw-bold fs-2 text-center">9</div>
    <div @click="multiply" class="btn operator bg-danger fs-2 text-center p-1">x</div>
    <div @click="append('4')" class="btn fw-bold fs-2 text-center">4</div>
    <div @click="append('5')" class="btn fw-bold fs-2 text-center">5</div>
    <div @click="append('6')" class="btn fw-bold fs-2 text-center">6</div>
    <div @click="minus" class="btn operator bg-danger fs-2 text-center p-1">-</div>
    <div @click="append('1')" class="btn fw-bold fs-2 text-center">1</div>
    <div @click="append('2')" class="btn fw-bold fs-2 text-center">2</div>
    <div @click="append('3')" class="btn fw-bold fs-2 text-center">3</div>
    <div @click="plus" class="btn operator bg-danger fs-2 text-center p-1">+</div>
    <div @click="append('0')" class="btn zero fw-bold fs-2 text-center">0</div>
    <div @click="dot" class="btn">.</div>
    <div @click="equal" class="btn  operator text-dark fs-3 text-center">=</div>
  </div>
 </div>
</template>

<script>
export default {
  data() {
    return {
      previous: null,
      current: '',
      operator: null,
      operatorClicked: false,
    }
  },
  methods: {
    clear() {
      this.current = '';
    },
    sign() {
      this.current = this.current.charAt(0) === '-' ? 
        this.current.slice(1) : `-${this.current}`;
    },
    square() {
      this.current = `${parseFloat(this.current) * this.current}`;
    },
    append(number) {
      if (this.operatorClicked) {
        this.current = '';
        this.operatorClicked = false;
      }
      this.current = `${this.current}${number}`;
    },
    dot() {
      if (this.current.indexOf('.') === -1) {
        this.append('.');
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
    multiply() {
      this.operator = (a, b) => a * b;
      this.setPrevious();
    },
    minus() {
      this.operator = (a, b) => a - b;
      this.setPrevious();
    },
    plus() {
      this.operator = (a, b) => a + b;
      this.setPrevious();
    },
    equal() {
      this.current = `${this.operator(
        parseFloat(this.current), 
        parseFloat(this.previous)
      )}`;
      this.previous = null;
    }
  }
}
</script>

<style scoped>

.calculator {
  margin: 0 auto;
  width: 400px;
  font-size: 40px;
  display: grid;
  grid-template-columns: repeat(4, 1fr);
  grid-auto-rows: minmax(50px, auto);
}

.display {
  grid-column: 1 / 5;
  color: white;
}

.zero {
  grid-column: 1 / 3;
  
}


.btn:hover {
  background-color: #e42828;
  
}


.btn {
  background-color: #a18585;
  border: 1px solid #999;
}

.operator {
  color: rgb(30, 233, 8);
}
.operator:hover {
  color: rgb(192, 31, 31);
}

</style>