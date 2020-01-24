<template>
  <div id="app">
    
    <CustomText />
      <!-- Sidebar 
      <aside id="aside">
        <div>Things to see:</div>
          <ul>
            <li>one</li>
            <li>two</li>
          </ul>
      </aside>

      Main 
      <main id="main">
          <CustomText />
      </main>-->
  </div>
</template>

<script>
import CustomText from './components/CustomText.vue'

export default {
  name: 'app',
  components: {
    CustomText
  }
}
</script>

<style>

#app {
  font-family: 'Avenir', Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  display: flex;
  color: #2c3e50;
  margin: 100px 200px;
}

#aside {
  border: solid 1px gray;
  width: 200px;
  padding: 20px;
}

#main {
  border: solid 1px gray;
  flex: 1;
  overflow: auto;
  padding: 20px;
}
</style>
