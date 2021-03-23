 <template>
  <section class="produtos-container">
    <div v-for="{ id, nome, preco, descricao, fotos } in produtos" :key="id">
      <img v-if="fotos" :src="fotos[0].src" :alt="fotos[0].titulo" />
      <p class="preco">{{ preco }}</p>
      <h2 class="titulo">{{ nome }}</h2>
      <p>{{ descricao }}</p>
    </div>
  </section>
</template>

<script>
export default {
  data() {
    return {
      produtos: null,
    };
  },
  methods: {
    getProdutos() {
      fetch("http://localhost:3000/produto")
        .then((r) => r.json())
        .then((r) => {
          this.produtos = r;
        });
    },
  },
  created() {
    this.getProdutos();
  },
};
</script>

<style>
</style>