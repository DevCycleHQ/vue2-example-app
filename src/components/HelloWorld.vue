<template>
  <div class="hello">
    <h1>{{ msg }}</h1>
    <div v-if="test">
      Feature Flag Enabled
    </div>
  </div>
</template>

<script>
import { initialize } from '@devcycle/devcycle-js-sdk'

const user = { user_id: '123' }
const dvcOptions = { logLevel: 'debug' }
const dvcClient = initialize('CLIENT_TOKEN', user, dvcOptions)

export default {
  name: 'HelloWorld',
  props: {
    msg: String
  },
  data() {
    return {
      test: false
    }
  },
  mounted () {
    dvcClient.onClientInitialized().then(() => {
      this.test = dvcClient.variable('test', false).value
    })
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
