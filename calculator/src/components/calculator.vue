<template>
    <h1 >   calculator</h1>
    <div class="p-3" style="max-width:400px; margin:50px auto ;background :#dbf0f9">
    <div class="w-full rounded m-1 p-3 text-right text-white bg-vue-dark">
      {{calcultorValue || 0}}
    </div>
   
  
  <div class="row no-gutters">
    <div class="col-3" v-for="n in calculatorEelements" :key="n">
      <div class="lead text-white text-center m-1 py-3 bg-vue-dark hover-effect "
      :class="{'bg-vue-green': ['C','*','/','-','+','%','='].includes(n)}"	
        @click="action(n)"
>
      {{n}}
      </div>
    </div>
  </div>
 </div>

</template>

<script>
export default {
  name: 'HelloWorld',
  props: {
    msg: String
  },
  data(){
    return{
      calcultorValue:'',
      calculatorEelements:['c','*','/','-',7,8,9,'+',4,5,6,'%',1,2,3,'=',0,'.'],
      operator: null,
      previousCalculatorValue:'',
    }
     },
    methods: {
      action(n){
         /*appent value*/

        if(!isNaN(n)  || n==='.'){
          this.calcultorValue += n + '';
        }

        // clear value
        if(n ==='c') {
          this .calcultorValue = '';

        }

        // percentage
       if(n === '%'){
        this.calcultorValue = this.calcultorValue /  100 + '';
       }

      
       if (['/','*','-','+'].includes(n)){
        this.operator =n;
        this.previousCalculatorValue = this.calcultorValue;
        this.calculatorValue  = '';
               }

      // equqlto
     if(n=== '='){
      this.calcultorValue =eval(
        this.previousCalculatorValue + this.operator + this.calcultorValue
      );
      
      this.previousCalculatorValue ='';
      this.operator =null;

     }

      }

    }

}
</script>

<style scoped>
.bg-vue-dark{
  background:grey;
}

.hover-effect:hover{
  background:darkgray;
  cursor: pointer;
}
.bg-vue-green{
  background:#3f628b;
}
h1{
  text-align: center;
  margin-top: 90px;
}
</style>
