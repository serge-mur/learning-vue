<template>
  <div class="form-group">
      <label>
          {{ name }}
          <span
              v-if="activated"
              class="fa"
              :class="iconClasses"
              >
          </span>
      </label>
      <input type="text" class="form-control" :value="value" @input="onInput">
  </div>
</template>

<script>
export default {
  name: 'AppField',
  props: ['name', 'value', 'valid'],
  data() {
      return {
          activated: this.value !== ''
      }
  },
  computed: {
      iconClasses() {
          return {
              'fa-circle-check text-success': this.valid,
              'fa-circle-check text-danger': !this.valid
          }
      }
  },
  methods: {
      onInput(e) {
          this.activated = true
          this.$emit('updated', e.target.value)
          console.log(e)
      }
  }

}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>

</style>
