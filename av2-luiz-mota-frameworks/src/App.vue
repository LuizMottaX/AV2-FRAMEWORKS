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

function removerProduto(id) {
  produtos.value = produtos.value.filter(p => p.id !== id)
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

    <div v-if="produtos.length > 0" class="lista-area">
      <h2>Minha Cesta de Compras</h2>
      <p class="contador">{{ produtos.length }} {{ produtos.length === 1 ? 'item' : 'itens' }} na cesta</p>
      <ul>
        <li v-for="produto in produtos" :key="produto.id">
          <span>{{ produto.nome }}</span>
          <button class="btn-remover" @click="removerProduto(produto.id)">Remover</button>
        </li>
      </ul>
    </div>

    <div v-else class="vazio">
      <p>Sua cesta está vazia! Adicione produtos para começar.</p>
    </div>
  </div>
</template>

<style scoped>
</style>
