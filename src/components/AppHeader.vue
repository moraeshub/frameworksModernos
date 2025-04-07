<template>
    <v-app-bar color="primary" dark>
      <v-app-bar-title>LIstar Salas</v-app-bar-title>
  
      <v-spacer />
  
      <v-btn variant="text" to="/salas" exact :active="route.path === '/salas'">
        Salas
      </v-btn>
  
      <v-divider vertical class="mx-3" />
  
      <v-btn variant="outlined" color="white" @click="logout">
        Sair
      </v-btn>
    </v-app-bar>
  </template>
  
  <script setup lang="ts">
  import { useRouter, useRoute } from 'vue-router'
  
  const router = useRouter()
  const route = useRoute()
  
  function logout() {
    localStorage.removeItem('auth')
    router.push('/Login')
  }
  </script>
  