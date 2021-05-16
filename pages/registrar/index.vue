<template>
  <div>
    <h1>Registre-se</h1>
    <p>Informe os dados abaixo para se registrar</p>

    <b-form @submit.prevent="register">
      <b-form-group>
        <b-form-input
          v-model="nome"
          type="text"
          placeholder="Nome"
          required
        ></b-form-input>
      </b-form-group>
      <b-form-group>
        <b-form-input
          v-model="email"
          type="email"
          placeholder="E-mail"
          required
        ></b-form-input>
      </b-form-group>

      <b-form-group>
        <b-form-input
          v-model="senha"
          type="password"
          placeholder="Senha"
          required
        ></b-form-input>
      </b-form-group>

      <b-button block type="submit" variant="primary">Salvar</b-button>
    </b-form>
  </div>
</template>

<script>
export default {
  layout: "login",
  data() {
    return {
      nome: null,
      email: null,
      senha: null,
    };
  },
  methods: {
    async register() {
      try {
        await this.$axios
          .post("register/", {
            nome: this.nome,
            email: this.email,
            senha: this.senha,
          })
          .then((response) => {
            if (response) this.$router.push("/login");
          });
      } catch (e) {
        console.log(e);
      }
    },
  },
};
</script>

