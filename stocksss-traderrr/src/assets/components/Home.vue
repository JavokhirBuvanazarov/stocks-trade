<template>
    <div>
      <h1>Trade or View your Portfolio</h1>
      <p>You may Save & Load your data</p>
      <h6>Click on "End Day" to begin a New Day</h6>
      <hr>
      <p>Your funds:  {{ funds | currency }}</p>
    </div>
</template>

<script>
    export default {
      computed:{
        funds(){
          return this.$store.getters.funds;
        }
      }
    }
</script>

<style scoped>

</style>
