<template>
  <td v-if="!renaming" @click="renamePractice">
    {{ name }}
  </td>
  <td v-else>
    <input type="text" v-model="newName" :placeholder="placeholder" />
    <div class="btn-group" role="group">
      <button class="btn btn-success btn-sm"
              @click="submitRename">
        确定
      </button>
      <button class="btn btn-secondary btn-sm"
              @click="cancelRename">
        取消
      </button>
    </div>
  </td>
</template>

<script>
import {defineComponent} from 'vue'

export default defineComponent({
  name: 'RenameableLabel',
  props: {
    name: String,
    placeholder: {
      type: String,
      default: '输入新的名称...'
    }
  },
  data() {
    return {
      renaming: false,
      newName: ''
    }
  },
  methods: {
    renamePractice() {
      this.newName = ''
      this.renaming = true
    },
    cancelRename() {
      this.newName = ''
      this.renaming = false
    },
    submitRename() {
      this.$emit('rename', this.newName)
      this.cancelRename()
    }
  }
})
</script>

<style scoped>

</style>
