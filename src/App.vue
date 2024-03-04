<script setup>

import { ref ,onMounted ,reactive} from 'vue';

const monedas = ref([
      { codigo: 'USD', texto: 'Dolar de Estados Unidos'},
      { codigo: 'MXN', texto: 'Peso Mexicano'},
      { codigo: 'EUR', texto: 'Euro'},
      { codigo: 'GBP', texto: 'Libra Esterlina'},
  ])

  const criptomonedas = ref([])
  const cotizar=reactive({
    moneda:'',
    criptomoneda:''
  })

  onMounted(()=>{
    const url = 'https://min-api.cryptocompare.com/data/top/mktcapfull?limit=20&tsym=USD'
    fetch(url)
     .then(response => response.json())
     .then(({Data}) => criptomonedas.value = Data)
  })
</script>

<template>
  <div class="contenedor">
    <h1 class="titulo">
      Cotizador de<span>Criptomonedas</span>

      <div class="contenido">
        <form class="formulario" action="">
          <div class="campo">
            <label for="moneda">Moneda:</label>
            <select name="" id="moneda" v-model="cotizar.moneda">
              <option value="">--Selecciona--</option>
              <option v-for="moneda in monedas" :value="moneda.codigo">{{moneda.texto}}</option>
            </select>
          </div>

          <div class="campo">
            <label for="crypto">Criptomonedas:</label>
            <select name="" id="crypto" v-model="cotizar.criptomoneda">
              <option value="">--Selecciona--</option>
              <option v-for="crypto in criptomonedas" :value="crypto.CoinInfo.Name">{{crypto.CoinInfo.FullName}}</option>
            </select>
          </div>

          <input type="submit" value="Cotizar">

        </form>
      </div>
    </h1>
  </div>
</template>

<style scoped></style>