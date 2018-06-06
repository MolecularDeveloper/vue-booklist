<template>
  <div class="hello">
    <h1>{{ msg }}</h1>
    <h2>Other Info</h2>
    <ul>
      <li>
        <a
          href="http://intellectualdark.website/"
          target="_blank"
        >
          Intellectual Dark Web
        </a>
      </li>
      <li>
        <a
          href="https://jordanbpeterson.com/category/reading-list/"
          target="_blank"
        >
         jp reading list
        </a>
      </li>
      <li>
        <a
          href="https://quillette.com/"
          target="_blank"
        >
          Quillette Articles
        </a>
      </li>
    </ul>
  </div>
</template>

<script>
export default {
  name: 'HelloWorld',
  data () {
    return {
      msg: 'Reading List'
    }
  }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
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
</style>
