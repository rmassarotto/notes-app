<template>
  <div>
    <h1>Notes App</h1>
    <p>Informe os dados abaixo para acessar</p>

    <b-form @submit.prevent="login">
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

      <b-button block type="submit" variant="primary">Acessar</b-button>
      <b-button block href="/registrar" variant="success">Registrar</b-button>
    </b-form>
  </div>
</template>

<script>
export default {
  layout: "login",
  data() {
    return {
      email: null,
      senha: null,
    };
  },
  methods: {
    async login() {
      try {
        await this.$auth.loginWith("local", {
          data: {
            email: this.email,
            senha: this.senha,
          },
        });

        this.$router.push("/");
      } catch (e) {
        console.log(e);
      }
    },
  },
};
</script>
