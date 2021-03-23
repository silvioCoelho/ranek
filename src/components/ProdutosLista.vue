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
import { api } from "@/services.js";
import { serialize } from "@/helpers.js";

export default {
  data() {
    return {
      produtos: null,
      produtosPorPagina: 9,
    };
  },
  computed: {
    url() {
      const query = serialize(this.$route.query);

      return `/produto?_limit=10${this.produtosPorPagina}${query}`;
    },
  },
  methods: {
    getProdutos() {
      api.get(this.url).then((r) => {
        this.produtos = r.data;
      });
    },
  },
  watch: {
    url() {
      this.getProdutos();
    },
  },
  created() {
    this.getProdutos();
  },
};
</script>

<style>
</style>