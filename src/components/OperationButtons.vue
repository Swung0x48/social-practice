<template>
  <td>
    <div class="btn-group" role="group">
      <button class="btn btn-danger" type="button"
              @click="deleteHandler">
        删除
      </button>
      <button v-if="ended"
              class="btn btn-dark" type="button"
              @click="endHandler">
        结束
      </button>
    </div>
  </td>
</template>

<script>
import {defineComponent} from 'vue'

export default defineComponent({
  name: 'OperationButtons',
  props: {
    ended: Boolean
  },
  methods: {
    deleteHandler() {
      this.$emit('delete')
    },
    endHandler() {
      this.$emit('end')
    }
  }
})
</script>

<style scoped>

</style>
