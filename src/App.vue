<script>
import TopMenu from './components/TopMenu'
export default {
  components: {
    TopMenu
  },
  created () {
    console.log('Created')
  }
}
</script>

<template>
<div>
<top-menu></top-menu>
<router-view></router-view>
</div>
</template>


<style>
@import './assets/bootstrap.min.css'

html {
  height: 100%;
}

body {
  display: flex;
  align-items: center;
  justify-content: center;
  height: 100%;
}

#app {
  color: #2c3e50;
  margin-top: -100px;
  max-width: 600px;
  font-family: Source Sans Pro, Helvetica, sans-serif;
  text-align: center;
}

#app a {
  color: #42b983;
  text-decoration: none;
}

.logo {
  width: 100px;
  height: 100px
}
</style>
