<template>
  <v-app>
    <h1 class="display-2 text-xs-center mt-4">福井県のイベント</h1>
    <v-content>
      <Events/>
    </v-content>
  </v-app>
</template>

<script>
import Events from './components/Events'

export default {
  name: 'App',
  components: {
    Events
  }
}
</script>
