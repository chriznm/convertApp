<script setup lang="ts">
let pzs: number = 1
let precioSetWon: number = 40000
let envio: number = 1800
let fee: number = 2000
let krw: number = 1
let usd: number = 0.000869565217391304
let mxn: number = 17.1325
let wonTotal: number = fee + precioSetWon + envio
let setEnUsd: number = Math.round(wonTotal * usd * 100) / 100
let setEnMxn: number = Math.round(setEnUsd * mxn)
let precioPCMxn: number = setEnMxn / pzs
let precioFinalPorSet: number = Math.round(precioPCMxn * 1.334)
let precioFinalPorPc: number = precioFinalPorSet / pzs
let ganancia: number = precioFinalPorPc - setEnMxn
</script>

<template>
  <div class="classContainer">
    <div>
      <v-text-field v-model="pzs" label="PZS" width="500px" />
      <v-text-field v-model="precioSetWon" label="Precio Set Won" width="500px" />
      <v-text-field v-model="envio" label="Envio" width="500px" />
      <v-text-field v-model="fee" label="FEE" width="500px" />
      <v-text-field v-model="wonTotal" label="WON TOTAL" width="500px" :readonly="true" />
      <v-text-field v-model="setEnUsd" label="SET EN USD" width="500px" />
      <v-text-field v-model="setEnMxn" label="SET EN MXN" width="500px" />
      <v-text-field v-model="precioPCMxn" label="Precio PC mxn" width="500px" />
      <v-text-field v-model="precioFinalPorSet" label="PRECIO FINAL POR SET" width="500px" />
      <v-text-field v-model="precioFinalPorPc" label="PRECIO FINAL POR PC" width="500px" />
      <v-text-field v-model="ganancia" label="GANANCIA" width="500px" />
    </div>
    <div class="tableClass">
      <v-text-field v-model="krw" label="KRW" width="500px" />
      <v-text-field v-model="usd" label="USD" width="500px" />
      <v-text-field v-model="mxn" label="MXN" width="500px" />
    </div>
  </div>
</template>

<style scoped>
.classContainer {
  display: flex;
}
.tableClass {
  margin-left: 100px;
}
</style>
