<script setup>
import { reactive } from 'vue';

const nome = 'maicon santana'
const meuObj = {
  nome:"maicon",
  filmeFavorito:"Harry Potter"
}

function dizOla(nome){
  return `${nome} diz oi`;
}

const enderecoDaImagemDoAndroid = "https://th.bing.com/th/id/OIP.pr3gbhcDVG4XQ00VOoCMlQHaEK?w=186&h=104&c=7&r=0&o=5&pid=1.7"
const imagemAndroid17 = "https://th.bing.com/th/id/OIP.lMDM-eTo0gCX3II1HrZhZwHaEK?w=186&h=104&c=7&r=0&o=5&pid=1.7"

const botaoEstaDesabilitado = false

const gostaDeDbz = true
const gostaDoAndroid17 = false

const estaAutorizado = false

//let contador = 0
const estado = reactive ({
  contador: 0,
  email: '',
  saldo: 5000,
  transferindo: 0,
})

function incrementar(){
  estado.contador++;
}

function decrementar(){
  estado.contador--;
}

function alteraEmail(evento){
  estado.email = evento.target.value;
}

function mostraSaldoFuturo () {
  const { saldo, transferindo } = estado;
  return saldo - transferindo;
}

function validaValorTransferencia() {
  const { saldo, transferindo } = estado;
  return saldo >= transferindo;
}

const nomes = [ 'maicon','iara','tati','bia'];

</script>

<template>
  <h1>{{ dizOla ("Android 16")}}</h1>
  <img v-if="gostaDeDbz" :src="enderecoDaImagemDoAndroid" alt="">
  <img v-else-if="gostaDoAndroid17" :src="imagemAndroid17" alt="">
  <h2 v-else>Não curte dos Androids De Dragon Ball Z</h2>

    <h1 v-if="estaAutorizado">Bem Vindo!</h1>
    <h1 v-else>Não possui acesso</h1>

  <br>
  <button :disabled="botaoEstaDesabilitado"> Enviar Mensagem </button> <!-- ! negação :disabled="!botaoEstaDesabilitado" -->

<br />
<hr />

{{ estado.contador }}

<button @click="incrementar" type="button">+</button>
<button @click="decrementar"  type="button">-</button>

<br />
<hr />

{{ estado.email }}
<input type="email" @keyup="alteraEmail">


<br />
<hr />

Saldo: {{ estado.saldo }} <br />
transferindo: {{ estado.transferindo }} <br />
Saldo depois da transferência: {{ mostraSaldoFuturo() }} <br />
<input class="campo" :class="{invalido: !validaValorTransferencia() }" @keyup="evento => estado.transferindo = evento.target.value" type="number" placeholder="Quantia para transferência" />
<button v-if="validaValorTransferencia()"> transferir</button>
<span v-else>valor maior que o saldo</span>
</template>


<br />
<hr />

<ul>
  <li>
  TESTE
  </li>
</ul>

<style scoped>
img {
  max-width: 200px;
}

.invalido{
  outline-color: red ;
  border-color: red;
}

.campo {
  border:  2px solid #000;
}
</style>
