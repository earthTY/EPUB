<template>
  <div id="app">
    <router-view/>
  </div>
</template>

<script>
export default {
  name: 'App'
}

document.addEventListener("DOMContentLoaded",()=>{
  const html = document.querySelector("html")
  let fontSize = window.innerWidth / 10

  html.style.fontSize = (fontSize > 50 ? 50 : fontSize) + "px"
})
</script>

<style>

</style>
