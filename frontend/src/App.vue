<template>
  <div>
    <div id="nav">
      <router-link to="/">Home</router-link> |
      <router-link to="/countries">Les pays</router-link> |
      <router-link to="/countryEdit">Edition pays</router-link> |
      <router-link to="/cityEdit">Edition villes</router-link> |
      <router-link to="/cityParPays">Villes par Pays</router-link> |
      <router-link to="/about">About</router-link> |
      <router-view />
    </div>
  </div>
</template>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
}

#nav {
  padding: 30px;
}

#nav a {
  font-weight: bold;
  color: #2c3e50;
}

#nav a.router-link-exact-active {
  color: #42b983;
}
</style>
