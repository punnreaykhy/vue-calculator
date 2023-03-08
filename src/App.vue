<template>
  <div id="app">
    <div class="container">
      <table>
        <tr>
          <td colspan="5">
            <div id="screen">
              <span id="screen_top">M=<span v-text="memory"></span></span>
              <div id="screen_bottom">
                <!-- v-text is a directive that is used to replace the content of HTML tag with private data -->
                <!-- It will update the content automatically when data is changed. It is called data reactive -->
                <span v-text="input_output" id="operand1" >0</span>
              </div>
              <!-- <span id="screen_bottom">0</span> -->
            </div>
          </td>
        </tr>
        <tr>
          <td>
            <button type="button" class="btn btn-warning" @click="mClear()">MC</button>
          </td>
          <td>
            <button type="button" class="btn btn-warning" @click="mRead()">MR</button>
          </td>
          <td>
            <button type="button" class="btn btn-warning" @click="mMinus()">M-</button>
          </td>
          <td>
            <button type="button" class="btn btn-warning" @click="mAdd()">M+</button>
          </td>
          <td>
            <button type="button" class="btn btn-light"  @click="backward()">
              <i class="fa fa-long-arrow-right" aria-hidden="true"></i>
            </button>
          </td>
        </tr>
        <tr>
          <td>
            <button type="button" class="btn btn-light" @click="showNumber('7')">7</button>
          </td>
          <td>
            <button type="button" class="btn btn-light" @click="showNumber('8')">8</button>
          </td>
          <td>
            <button type="button" class="btn btn-light" @click="showNumber('9')">9</button>
          </td>
          <td>
            <button type="button" class="btn btn-secondary" @click="showOperation('/')">÷</button>
          </td>
          <td>
            <button type="button" class="btn btn-light" @click="addNegative()">+/-</button>
          </td>
        </tr>
        <tr>
          <td>
            <button type="button" class="btn btn-light" @click="showNumber('4')">4</button>
          </td>
          <td>
            <button type="button" class="btn btn-light" @click="showNumber('5')">5</button>
          </td>
          <td>
            <button type="button" class="btn btn-light" @click="showNumber('6')">6</button>
          </td>
          <td>
            <button type="button" class="btn btn-secondary" @click="showOperation('*')">x</button>
          </td>
          <td>
            <button type="button" class="btn btn-secondary" @click="showOperation('-')">-</button>
          </td>
        </tr>
        <tr>
          <td>
            <button
              @click="showNumber(1)"
              type="button"
              class="btn btn-light"
            >
              1
            </button>
          </td>
          <td>
            <button type="button" class="btn btn-light" @click="showNumber('2')">2</button>
          </td>
          <td>
            <button type="button" class="btn btn-light" @click="showNumber('3')">3</button>
          </td>
          <td rowspan="2">
            <button type="button" class="btn btn-secondary long-btn" @click="showOperation('+')">+</button>
          </td>
          <td rowspan="2">
            <button type="button" class="btn btn-primary long-btn" @click="$event => doOperation()">=</button>
          </td>
        </tr>
        <tr>
          <td>
            <button type="button" class="btn btn-danger" @click="$event => clear()">C</button>
          </td>
          <td>
            <button type="button" class="btn btn-light" @click="showNumber('0')">0</button>
          </td>
          <td>
            <button type="button" class="btn btn-light" @click="showNumber('.')">.</button>
          </td>
        </tr>
      </table>
    </div>
    <div class="alert alert-danger" id="message_panel" role="alert">
      something wrong here
    </div>
  </div>
</template>

<script>
export default {
  name: 'App',
  components: {},
  data() {
    return {
      state: false,
      input_output: "",
      memory: 0,
    };
  },
  methods: {
    showNumber(number) {
      this.input_output += number;
      if(this.input_output[0] == 0 && this.input_output[1] != "."){
        this.input_output = this.input_output.slice(0, -1);
      }
    },
    showOperation( operator ) {
      this.doOperation();
      this.input_output += operator;
    },
    doOperation(){
      this.input_output = eval(this.input_output);
    },
    addNegative(){
      this.input_output = '-' + this.input_output;
    },
    clear () {
      this.input_output = "";
    },
    mAdd () {
      this.memory = eval(this.memory + "+" + this.input_output);
    },
    mMinus () {
      this.memory = eval(this.memory + "-" + this.input_output);
    },
    mRead () {
      if(this.memory != 0){
        if(this.input_output[(this.input_output.length)-1] == "+" || this.input_output[(this.input_output.length)-1] == "-" || this.input_output[(this.input_output.length)-1] == "*" || this.input_output[(this.input_output.length)-1] == "/"){
          this.input_output += this.memory;
        }  
      }
    },
    mClear () {
      this.memory = 0;
    },
    backward () {
      
        this.input_output = this.input_output.slice(0, -1);
      
    }
  },
};
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #304152;
  margin-top: 65px;
}
.container {
  margin-top: 10em;
  width: 300px;
  border: 3px solid black;
  padding-top: 20px;
  padding-bottom: 20px;
}
table {
  border-spacing: 7px;
  border-collapse: separate;
}
#screen {
  border: 1px solid black;
  padding: 7px;
  width: 255px;
  height: 4em;
}
#screen_top {
  display: block;
  font-size: 0.8rem;
  font-weight: bold;
}
#screen_bottom {
  font-size: 1.8rem;
  display: block;
  text-align: right;
}
#operand2 {
  background-color: skyblue;
}
.button-row {
  display: flex;
  justify-content: space-between;
}
button {
  width: 45px;
}
.long-btn {
  display: inline-block;
  height: 80px;
}
/* Message panel */
#message_panel {
  width: 300px;
  margin-top: 1em;
  display: none;
  margin-left: auto;
  margin-right: auto;
}
</style>
