<template>
  <q-layout>
    <q-page-container>
      <div id="app">
        <nav>
          <router-link to="/">Home</router-link>
          <router-link to="/register">Register</router-link>
          <router-link to="/login">Login</router-link>
        </nav>

        <router-view />
      </div>
    </q-page-container>
  </q-layout>
</template>

<script>
export default {};
</script>
