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
* {
  margin: 0;
  padding: 0;
  box-sizing: border-box;
}

.container {
  max-width: 520px;
  margin: 60px auto;
  padding: 40px 32px;
  font-family: 'Segoe UI', sans-serif;
  background: linear-gradient(135deg, #1a1a2e 0%, #16213e 100%);
  border-radius: 20px;
  box-shadow: 0 20px 60px rgba(0, 0, 0, 0.4);
  color: #e0e0e0;
}

h1 {
  text-align: center;
  font-size: 1.8rem;
  margin-bottom: 28px;
  background: linear-gradient(90deg, #e94560, #0f3460);
  -webkit-background-clip: text;
  -webkit-text-fill-color: transparent;
  background-clip: text;
}

.input-area {
  display: flex;
  gap: 10px;
  margin-bottom: 28px;
}

.input-area input {
  flex: 1;
  padding: 12px 16px;
  border: 2px solid #0f3460;
  border-radius: 12px;
  background: #1a1a2e;
  color: #e0e0e0;
  font-size: 0.95rem;
  outline: none;
  transition: border-color 0.3s;
}

.input-area input:focus {
  border-color: #e94560;
}

.input-area input::placeholder {
  color: #555;
}

.input-area button {
  padding: 12px 22px;
  background: linear-gradient(135deg, #e94560, #c23152);
  color: #fff;
  border: none;
  border-radius: 12px;
  font-size: 0.95rem;
  font-weight: 600;
  cursor: pointer;
  transition: transform 0.2s, box-shadow 0.2s;
}

.input-area button:hover {
  transform: translateY(-2px);
  box-shadow: 0 6px 20px rgba(233, 69, 96, 0.4);
}

.input-area button:active {
  transform: translateY(0);
}

h2 {
  font-size: 1.2rem;
  margin-bottom: 6px;
  color: #e94560;
}

.contador {
  font-size: 0.85rem;
  color: #8a8a9a;
  margin-bottom: 16px;
}

ul {
  list-style: none;
  display: flex;
  flex-direction: column;
  gap: 10px;
}

li {
  display: flex;
  justify-content: space-between;
  align-items: center;
  padding: 14px 18px;
  background: rgba(15, 52, 96, 0.35);
  border-radius: 12px;
  border: 1px solid rgba(15, 52, 96, 0.5);
  transition: background 0.2s, transform 0.15s;
}

li:hover {
  background: rgba(15, 52, 96, 0.55);
  transform: translateX(4px);
}

li span {
  font-size: 1rem;
}

.btn-remover {
  padding: 6px 14px;
  background: transparent;
  color: #e94560;
  border: 1px solid #e94560;
  border-radius: 8px;
  font-size: 0.8rem;
  cursor: pointer;
  transition: background 0.2s, color 0.2s;
}

.btn-remover:hover {
  background: #e94560;
  color: #fff;
}

.vazio {
  text-align: center;
  padding: 40px 20px;
  background: rgba(15, 52, 96, 0.2);
  border-radius: 16px;
  border: 2px dashed #0f3460;
}

.vazio p {
  color: #8a8a9a;
  font-size: 1rem;
}
</style>
