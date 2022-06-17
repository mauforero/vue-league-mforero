<template>
  <div id="app" class="mt-6 antialiased text-gray-700">
    <div class="container text-left mx-auto">
      <img alt="Vue logo" src="./assets/logo.png" class="w-16 inline-block">
      <h1 class="inline-block px-4 text-xl font-bold">Teams Local Time Tracker</h1>
    </div>
    <TeamDashboard />
  </div>
</template>

<script>
import TeamDashboard from './components/TeamDashboard.vue'

export default {
  name: 'App',
  components: {
    TeamDashboard
  }
}
</script>
