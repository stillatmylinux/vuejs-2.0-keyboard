<template>
  <div class="screen">
    <textarea v-model="screen"></textarea>
  </div>
</template>

<script>
export default {
  name: 'Screen',
  props: [
    'screen'
  ]
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style>
.screen textarea {
 width: 688px;
 height: 200px;
}
</style>
