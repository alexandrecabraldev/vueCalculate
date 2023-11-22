
<script setup>
  import { reactive } from 'vue';
  import { watch } from 'vue';

    const store = reactive({
      selectValue:'',
      inputNumber1Value:'',
      inputNumber2Value: '',
      result: 0,

      multiplicacao(){
        this.result= Number(this.inputNumber1Value) * Number(this.inputNumber2Value);
      },

      divisao(){
        this.result= Number(this.inputNumber1Value) / Number(this.inputNumber2Value);
      },

      adicao(){
        this.result= Number(this.inputNumber1Value) + Number(this.inputNumber2Value);
      },

      subtracao(){
        this.result= Number(this.inputNumber1Value) - Number(this.inputNumber2Value);
      },

    })

    function inputNumber1(event){
      store.inputNumber1Value=event.target.value
      console.log(event.target.value);
    }

    function inputNumber2(event){
      store.inputNumber2Value=event.target.value
      console.log(event.target.value);
    }

    function handleSelect(event){
      store.selectValue= event.target.value;
      switch(store.selectValue){
        case 'multiplicacao': store.multiplicacao()
      }
      console.log(store.selectValue)
    }

    watch(
          [() => store.inputNumber1Value, () => store.inputNumber2Value, () => store.selectValue], 
            () => {
              switch(store.selectValue){
                case 'multiplicacao': store.multiplicacao(); break;
                case 'divisao':store.divisao();break;
                case 'adicao': store.adicao(); break;
                case 'subtracao':store.subtracao();break;
        }
      }, { immediate: true }
    )
    
</script>

<template>

  <main>
    <input type="number" @keyup="inputNumber1"/>
    <input type="number" @keyup="inputNumber2"/>

    <select name="operacao" @change="handleSelect">
      <option selected disabled>Operação</option>
      <option value="adicao">Adição</option>
      <option value="subtracao">Subtração</option>
      <option value="divisao">Divisão</option>
      <option value="multiplicacao">Multiplicação</option>
    </select>

    <span>Reulstado: {{ store.result }}</span>
  </main>
  
</template>

<style scoped>

  input{
    padding: 4px;
    border: 0.1px solid black;
    border-radius: 4px;
  }

  input::-webkit-inner-spin-button, input::-webkit-outer-spin-button{
    -webkit-appearance: none;
    
  }

  input[type=number]{
    -moz-appearance: none;
  }

  main{
    display: inline-flex;
    gap: 12px;
    border: 1px solid black;
    border-radius: 8px;
    padding: 16px;
    align-items: center;
    
  }

  main > select{
    padding: 2px;
  }

</style>

<style>
 *{
    margin: 0;
    padding: 0;
    box-sizing: border-box;
  }

  #app{
    display: flex;
    justify-content: center;
    align-items: center;
    width: 100%;
    height: 100vh;
    
  }

</style>
