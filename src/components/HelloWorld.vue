<template>
  <div class="hello">
    <router-link to="Vote"><img class="image" src="../assets/logo.png"></router-link>
    <h1>{{ msg }}</h1>
  </div>
</template>

<script>
export default {
  name: 'HelloWorld',
  data () {
    return {
      msg: 'Voting App, press on logo to proceed'
    }
  }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
.hello{
  position: relative;
  width: 50%;
  margin: auto;
  height: 50%;
  text-align: center;
  padding: 17% 0px 17% 0px;
}
h1, h2 {
  font-weight: normal;
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
@keyframes example {
     100% { -webkit-transform: rotate(360deg); transform:rotate(360deg); }
}

/* The element to apply the animation to */
.image {
    animation-name: example;
    animation-duration: 4s;
}
</style>
