<script setup>
import { reactive } from 'vue';

const nome = 'Luis'
const objeto = {
  nome: 'Luis',
  filmeFav: 'LOTR'
}
function dizOi(nome){
  return `${nome} manda saudações`
}

const endereçoImg = 'https://encrypted-tbn0.gstatic.com/images?q=tbn:ANd9GcQnlc094v-eqQk6mEwV4vaoR175Kpn0CvFpaA&usqp=CAU'
const endereço2 = 'https://encrypted-tbn0.gstatic.com/images?q=tbn:ANd9GcQEvBN7IxAlEug19rKKpM77UuBtqZQKpnnkjg&usqp=CAU'
const imgSandman = 'https://tm.ibxk.com.br/2021/09/02/02122234915186.jpg'

const btnHabilitado = false

const gostaDoHellboy = false
const gostaDoSandman = true

const estaAutorizado = true

// let contador = 0

const estado = reactive({
  contador: 0,
  email: '',
  saldo: 5000,
  transferindo: 0,
  nomes: ['Joao', 'Paulo', 'Luisa', 'Monica'],
  nomeInserido: '',
})

function incrementar(){
  estado.contador++
}

function decrementar(){
  estado.contador--
}

function alteraEmail(evento) {
  estado.email = evento.target.value
} 

function novoSaldo(){
  const {saldo, transferindo} = estado //usando a desestruturação
  return saldo - transferindo
}

function validaTransferencia(){
  const {saldo, transferindo} = estado //usando a desestruturação
  return saldo >= transferindo
}

function cadastraNome(){
  if(estado.nomeInserido.length >= 3){
    estado.nomes.push(estado.nomeInserido)
  } else {
    alert('Digite mais caracteres')
  }
}
</script>

<template>
<h1>{{ nome }}</h1>
<h2>{{ 10 + 20 }}</h2>
<h3>{{ objeto.filmeFav }}</h3>
<h4>{{ dizOi('Curió') }}</h4>
<img v-bind:src="endereçoImg" alt="">
<img v-if="!gostaDoHellboy" :src="endereço2" alt="">
<img v-else-if="!gostaDoSandman" :src="imgSandman" alt="">
<h2 v-else>Não curte Dark Fantasy</h2>
<!-- o v-if não renderiza a tag, ou seja, ela não aparece ao inspecionar o DOM. Já o v-show apenas troca o display entre block e none -->

<h1 v-if="!estaAutorizado">Bem vindo Batman</h1>
<h1 v-else>Acesso negado</h1>

<button :disabled="!btnHabilitado">Enviar mensagem</button>

<br>
<hr>

{{ estado.contador }}

<button @click="incrementar" type="button">+</button>
<button @click="decrementar" type="button">-</button>

<br>
<hr>

{{ estado.email }}

<input type="email" @keyup= "alteraEmail">

<br>
<hr>

Saldo: {{ estado.saldo }}
<br>
Transferindo: {{ estado.transferindo }}
<br>
Novo Saldo: {{ novoSaldo() }}
<br>

<input type="number" placeholder="Quantia a ser transferida"  :class="{invalido: !validaTransferencia()}" class="campo" @keyup="evento => estado.transferindo = evento.target.value">
<br>
<button v-if="validaTransferencia()">Transferir</button>
<span v-else>Valor excede o saldo</span>

<br>
<hr>

<ul>
  <li v-for="nome in estado.nomes">
    {{ nome }}
  </li>
</ul>
<br>
<input type="text" placeholder="Digite um novo Nome" @keyup="evento => estado.nomeInserido = evento.target.value">
<button @click="cadastraNome()" type="button">Cadastrar nome</button>

<!-- o v-for pode ser usado em qualquer tag e não apenas na li -->

<h3 v-for="nome in estado.nomes">{{ nome }}</h3>
</template>

<style scoped>
img {
  max-width: 300px;
}

.invalido {
  border-color: red;
  outline-color: red;
}

.campo{
  border: 2px solid blue;
}
</style>
