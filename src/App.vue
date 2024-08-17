<template>
  <div id="app">
    <h1>Calculadora Aritmética</h1>
    <div>
      <input v-model.number="numero1" type="number" placeholder="Digite o primeiro número" />
      <input v-model.number="numero2" type="number" placeholder="Digite o segundo número" />
      
      <select v-model="operacao">
        <option value="+">Adicionar</option>
        <option value="-">Subtrair</option>
        <option value="*">Multiplicar</option>
        <option value="/">Dividir</option>
      </select>

      <p v-if="resultado !== null">Resultado: {{ resultado }}</p>
    </div>
  </div>
</template>

<script>
export default {
  data() {
    return {
      numero1: 0,
      numero2: 0,
      operacao: '+',
      resultado: null
    };
  },
  watch: {
    numero1: 'calcular',
    numero2: 'calcular',
    operacao: 'calcular'
  },
  methods: {
    calcular() {
      const num1 = parseFloat(this.numero1);
      const num2 = parseFloat(this.numero2);
      switch (this.operacao) {
        case '+':
          this.resultado = num1 + num2;
          break;
        case '-':
          this.resultado = num1 - num2;
          break;
        case '*':
          this.resultado = num1 * num2;
          break;
        case '/':
          if (num2 === 0) {
            this.resultado = 'Erro: Divisão por zero';
          } else {
            this.resultado = num1 / num2;
          }
          break;
        default:
          this.resultado = null;
      }
    }
  },
  mounted() {
    this.calcular(); // Calcular inicialmente com os valores padrão
  }
};
</script>

<style scoped>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}

input, select {
  margin: 5px;
  padding: 10px;
  font-size: 16px;
}
</style>
