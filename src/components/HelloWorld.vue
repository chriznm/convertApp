<template>
  <div class="classContainer">
    <div>
      <v-text-field v-model="quantity" label="PZS" width="500px" />
      <v-text-field v-model="precioSetWon" label="Precio Set Won" width="500px" />
      <v-text-field v-model="envio" label="Envio" width="500px" />
      <v-text-field v-model="fee" label="FEE" width="500px" />
      <v-text-field v-model="wonTotal" label="WON TOTAL" width="500px" :readonly="true" />
      <v-text-field v-model="setEnUsd" label="SET EN USD" width="500px" :readonly="true" />
      <v-text-field v-model="setEnMxn" label="SET EN MXN" width="500px" :readonly="true" />
      <v-text-field v-model="precioPCMxn" label="Precio PC mxn" width="500px" :readonly="true" />
      <v-text-field
        v-model="precioFinalPorSet"
        label="PRECIO FINAL POR SET"
        width="500px"
        :readonly="true"
      />
      <v-text-field
        v-model="precioFinalPorPc"
        label="PRECIO FINAL POR PC"
        width="500px"
        :readonly="true"
      />
      <v-text-field v-model="ganancia" label="GANANCIA" width="500px" :readonly="true" />
    </div>
    <div class="tableClass">
      <v-text-field v-model="krw" label="KRW" width="500px" />
      <v-text-field v-model="usd" label="USD" width="500px" />
      <v-text-field v-model="mxn" label="MXN" width="500px" />
    </div>
  </div>
</template>

<script setup lang="ts">
import { ref, computed, type Ref, type ComputedRef } from 'vue'

const quantity: Ref<number> = ref(1)
const precioSetWon: Ref<number | undefined> = ref()
const envio: Ref<number | undefined> = ref()
const fee: Ref<number | undefined> = ref()
const krw: Ref<number | undefined> = ref()
const usd: Ref<number | undefined> = ref()
const mxn: Ref<number | undefined> = ref()

const wonTotal: ComputedRef<number> = computed<number>(
  () => Number(fee.value) + Number(precioSetWon.value) + Number(envio.value) || 0
)
const setEnUsd: ComputedRef<number> = computed<number>(
  () => Math.round(wonTotal.value * Number(usd.value) * 100) / 100 || 0
)
const setEnMxn: ComputedRef<number> = computed<number>(
  () => Math.round(setEnUsd.value * Number(mxn.value)) || 0
)
const precioPCMxn: ComputedRef<number> = computed<number>(() => setEnMxn.value / quantity.value)
const precioFinalPorSet: ComputedRef<number> = computed<number>(() =>
  Math.round(precioPCMxn.value * 1.334)
)
const precioFinalPorPc: ComputedRef<number> = computed<number>(
  () => precioFinalPorSet.value / quantity.value
)
const ganancia: ComputedRef<number> = computed<number>(
  () => precioFinalPorPc.value - setEnMxn.value
)
</script>
<style scoped>
.classContainer {
  display: flex;
}
.tableClass {
  margin-left: 100px;
}
</style>
