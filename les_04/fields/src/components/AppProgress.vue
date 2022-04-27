<template>
    <div class="progress">
        <div class="progress-bar" role="progressbar" :style="{width: progressWidth}"></div>
    </div>
</template>

<script>
export default {
  name: 'AppProgress',
  props: ['progressWidth']
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>

</style>
