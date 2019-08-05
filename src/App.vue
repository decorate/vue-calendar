<template>
  <div id="app">
      <WeeklyCalendar ref="calendar"></WeeklyCalendar>
  </div>
</template>

<script>
    import WeeklyCalendar from './components/WeeklyCalendar'

    export default {
        components: {
            WeeklyCalendar
        },

        mounted() {
            const w = this.$refs.calendar.getWeekly()
            console.log(w)
            w[0][0].active = true
        },

        methods: {

        }
    }

</script>

<style>
#app {
    font-family: 'Avenir', Helvetica, Arial, sans-serif;
    -webkit-font-smoothing: antialiased;
    -moz-osx-font-smoothing: grayscale;
    text-align: center;
    color: #2c3e50;
    padding: 15px;
    max-width: 600px;
    margin: auto;
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
