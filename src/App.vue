<template>
  <div id="app">
    <router-view/>
  </div>
</template>

<style lang="scss">
  @import url('https://fonts.googleapis.com/css?family=Baloo+Chettan+2:400,500,700&display=swap');

#app {
  font-family: 'Baloo Chettan 2', Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #232323;
  display: flex;
  flex-direction: column;
  justify-content: flex-start;
  align-items: center;
}

  body {
    margin: 0;
    width: 100vw;
    min-height: 100vh;
  }
</style>
