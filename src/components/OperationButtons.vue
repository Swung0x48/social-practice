<template>
  <td>
    <div class="btn-group" role="group">
      <button v-if="joined === 0" class="btn btn-success" type="button"
              @click="joinHandler">
        加入
      </button>
      <button v-else-if="joined === 1" class="btn btn-success disabled" type="button">
        已加入
      </button>
      <button class="btn btn-danger" type="button"
              @click="deleteHandler">
        删除
      </button>
      <button v-if="state === 0"
              class="btn btn-dark" type="button"
              @click="endHandler">
        结束
      </button>
      <button v-else-if="state === 1"
              class="btn btn-dark disabled" type="button">
        已结束
      </button>
    </div>
  </td>
</template>

<script>
import {defineComponent} from 'vue'

export default defineComponent({
  name: 'OperationButtons',
  props: {
    state: {
      type: Number,
      required: true
    },
    joined: {
      type: Number,
      required: true
    },
  },
  computed: {
  },
  methods: {
    deleteHandler() {
      this.$emit('delete')
    },
    endHandler() {
      this.$emit('end')
    },
    joinHandler() {
      this.$emit('join')
    },
  }
})
</script>

<style scoped>

</style>
