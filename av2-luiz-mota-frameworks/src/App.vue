<script setup>
import { ref } from 'vue'

const novoProduto = ref('')
const produtos = ref([])

function adicionarProduto() {
  const nome = novoProduto.value.trim()
  if (!nome) return
  produtos.value.push({ id: Date.now(), nome })
  novoProduto.value = ''
}
</script>

<template>
  <div class="container">
    <h1>🛒 Gestão de Compras</h1>

    <div class="input-area">
      <input
        v-model="novoProduto"
        @keyup.enter="adicionarProduto"
        placeholder="Digite o nome do produto..."
      />
      <button @click="adicionarProduto">Adicionar</button>
    </div>
  </div>
</template>

<style scoped>
</style>
