<template>
  <div class="hello">
    <div v-if="funcName==='setServiceLabel'">
      <setServiceLabel v-bind="compData"/>
    </div>
    <div v-if="funcName==='commonSearch'">
      <commonSearch v-bind="compData"/>
    </div>
  </div>
</template>

<script>
import commonSearch from './commonSearch'
import setServiceLabel from './setServiceLabel'
export default {
  name: 'compSele',
  components:{
    commonSearch,
    setServiceLabel
  },
  props: {
    funcName: String,
    compData: Object
  }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
h3 {
  margin: 40px 0 0;
}
ul {
  list-style-type: none;
  padding: 0;
}
li {
  display: inline-block;
  margin: 0 10px;
}
a {
  color: #42b983;
}
</style>
