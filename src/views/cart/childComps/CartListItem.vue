<template>
  <div>
    {{product}}
  </div>
</template>

<script>
export default {
  name:'CartListItem',
  data () {
    return {
    }
  },
  props: {
    product: {
      type: Object,
      default() {
        return {}
      }
    }
  }
}
</script>

<style  scoped>

</style>
