<template>
    <div>
        <!-- <b-nav tabs>
          <b-nav-item active>Fancy Quiz App</b-nav-item>
          <b-nav-item>Counter: {{correctAnswers}}/{{totalAnswers}}</b-nav-item>
          <b-nav-item>Another Link</b-nav-item>
          <b-nav-item disabled>Disabled</b-nav-item> -->
        <!-- </b-nav> -->
        <b-navbar type="dark" variant="dark">
          <b-navbar-nav>
            <b-nav-item active>Fancy Quiz App</b-nav-item>
            <b-nav-item >Counter: {{correctAnswers}}/{{totalAnswers}}</b-nav-item>
      
            
          </b-navbar-nav>
        </b-navbar>
      </div>
</template>

<script>
export default{
  props:['correctAnswers',
    'totalAnswers']
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>

</style>