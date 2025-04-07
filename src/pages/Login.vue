<template>
  <div class="d-flex flex-column align-center">
    <v-card class="w-100 rounded-md" max-width="500">
      <v-card-title class="text-h5 text-center">Login</v-card-title>
      <v-card-text>
        <v-form @submit.prevent="handleLogin" ref="form">
          <v-text-field
            v-model="email"
            label="Email"
            type="email"
            required
            prepend-inner-icon="mdi-email"
          ></v-text-field>

          <v-text-field
            v-model="password"
            label="Senha"
            type="password"
            required
            prepend-inner-icon="mdi-lock"
          ></v-text-field>

          <v-btn type="submit" color="primary" block class="mt-4">Entrar</v-btn>
        </v-form>
      </v-card-text>
    </v-card>
  </div>
</template>

<script setup lang="ts">
import { ref } from "vue";
import { useRouter } from "vue-router";

const router = useRouter();

const email = ref("");
const password = ref("");

const handleLogin = () => {
  console.log("Email:", email.value);
  console.log("Senha:", password.value);
  localStorage.setItem("auth", "true");
  router.push("/Salas");
}
</script>
