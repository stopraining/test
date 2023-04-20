<template>
  <div>
    <h1>{{ msg }}</h1>
    <br>
    <div class="container flex-nowrap">
      <div class="row">
        <div class="col-md">
          <form action="#" class="main">
            <input class="show" type="text" v-model="showCal"><br><br>
            <input class="btn btn-info m-2" type="button" value="AC" @click="show">
            <input class="btn btn-info m-2" type="button" value="C" @click="show">
            <input class="btn btn-secondary m-2" type="button" value="▶️" @click="show">
            <input class="btn btn-secondary m-2" type="button" value="+/-" @click="show"><br>
            <input class="btn btn-secondary m-2" type="button" value="7" @click="show">
            <input class="btn btn-secondary m-2" type="button" value="8" @click="show">
            <input class="btn btn-secondary m-2" type="button" value="9" @click="show">
            <input class="btn btn-secondary m-2" type="button" value="÷" @click="operator"><br>
            <input class="btn btn-secondary m-2" type="button" value="4" @click="show">
            <input class="btn btn-secondary m-2" type="button" value="5" @click="show">
            <input class="btn btn-secondary m-2" type="button" value="6" @click="show">
            <input class="btn btn-secondary m-2" type="button" value="x" @click="operator"><br>
            <input class="btn btn-secondary m-2" type="button" value="1" @click="show">
            <input class="btn btn-secondary m-2" type="button" value="2" @click="show">
            <input class="btn btn-secondary m-2" type="button" value="3" @click="show">
            <input class="btn btn-secondary m-2" type="button" value="-" @click="operator"><br>
            <input class="btn btn-secondary m-2" type="button" value="." @click="show">
            <input class="btn btn-secondary m-2" type="button" value="0" @click="show">
            <input class="btn btn-secondary m-2" type="button" value="=" @click="equal">
            <input class="btn btn-secondary m-2" type="button" value="+" @click="operator"><br>
          </form>
        </div>
      </div>
    </div>
    
  </div>
</template>

<script>
export default {
  name: 'CalculatorArea',
  props: {
    msg: String
  },
  data(){
    return{
      showCal:'',
      totalString :'',

    }
  },
  methods:{
    show(val){

      if(val.target.value == 'AC'){ //all clean
        this.showCal = ''
        this.totalString = ''

      }else if(val.target.value =='C'){ //clean
        this.showCal = ''

      }else if(val.target.value =='▶️'){ //刪掉一數字
        this.showCal = this.showCal.slice(0,-1)

      }else if(val.target.value =='+/-'){ 
        console.log('+/-')
        this.showCal = Number(this.showCal)*(-1)

      }else if(this.showCal.length<15){ //15位數
        this.showCal += val.target.value

      } 

    },
    equal(){ //等號
      this.totalString += this.showCal
      this.showCal = eval(this.totalString)
      this.totalString = this.showCal

    },  
    operator(oper){  //運算符
      this.showCal = this.checkZero(this.showCal)
      this.totalString += this.showCal
      switch(oper.target.value){
        case '+':
          this.totalString += '+'
          this.showCal = ''
          break
        case '-': 
          if(this.showCal.length==0){
            this.showCal += '-'
          }else{
            console.log('mini')
            this.totalString += '-'
            this.showCal = ''
          }  
          break 
        case 'x':
          this.totalString += '*'
          this.showCal = ''
          break
        case '÷':
          this.totalString += '/'
          this.showCal = ''
          break
      }
    },
    checkZero(num){  
      if((/^0+/g).test(num)){
        num = Number(num)
        return num
      }
      return num
      
    }
  }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style lang="scss" scoped>


*{
  margin: auto;
  padding: auto;
}

.main{
  background-color: black;
  color: black;
  height: auto;
  width: 320px;
  padding: 20px;
  border-radius: 20px;
  box-shadow: 3px 3px 5px grey;
}
.btn{
  width: 50px;
} 
.show{
  background-color:darkgray;
  width: 255px;
  height: 50px;
  text-align: right;
  font-size: 20pt;
  font-family: 'Courier Prime', monospace;
  padding: 5px;
}


h1{
  color: cadetblue ;
}

@import "~bootstrap/scss/bootstrap";
@import url('https://fonts.googleapis.com/css2?family=Courier+Prime&display=swap'); 
</style>
