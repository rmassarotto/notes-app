<template>
  <div>
    <p v-if="$fetchState.pending" class="text-center">Carregando...</p>
    <p v-else-if="$fetchState.error" class="text-center">Ocorreu um erro :(</p>
    <div class="row">
      <div v-for="nota of notas" :key="nota.id" class="col-md-3">
        <div class="card bg-warning my-3">
          <div class="card-body">
            <h5 class="card-title">{{ nota.titulo }}</h5>
            <p v-if="nota.descricao" class="card-text">
              {{ nota.descricao }}
            </p>
          </div>
        </div>
      </div>
    </div>
  </div>
</template>
	
<script>
export default {
  layout: "home",
  middleware: "auth",
  data() {
    return {
      notas: [],
    };
  },

  async fetch() {
    const { data } = await this.$axios.get("nota/usuario/2");
    this.notas = data;
  },

  methods: {
    async logout() {
      await this.$auth.logout();
      this.$router.push("/login");
    },
  },
};
</script>

<style>
.card {
  min-height: 15rem;
}
</style>
