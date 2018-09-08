<template>
  <v-app>
    <Admin v-if="showAdmin"></Admin>
    <Project></Project>
  </v-app>
</template>

<script>
import HelloWorld from './components/HelloWorld'
import Project from './components/Project'
import Admin from './components/Admin'

export default {
  name: 'App',
  components: {
    HelloWorld,
    Project,
    Admin
  },
  data () {
    return {
      showAdmin: true
    }
  }
}
</script>
