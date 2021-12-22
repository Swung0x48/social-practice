<template>
  <tr>
    <td data-bs-toggle="collapse" :data-bs-target="`#${bsTarget}`">
      {{ group.groupID }}
    </td>
    <RenameableLabel
      :name="group.groupName"
      @rename="rename"
    />
    <td data-bs-toggle="collapse" :data-bs-target="`#${bsTarget}`">
      {{ group.practiceID }}
    </td>
    <td>
      <div class="btn-group" role="group">
        <button class="btn btn-danger" type="button"
                @click="leaveHandler">
          退出
        </button>
      </div>
    </td>
  </tr>
  <Collapse :bs-target="bsTarget">
    <slot></slot>
<!--    <UserTable :group-id="group.groupID" />-->
  </Collapse>
</template>

<script lang="ts">
import {defineComponent} from 'vue'
import RenameableLabel from '@/components/RenameableLabel.vue'
import {leaveGroup, renameGroup} from '@/services/group'
import Collapse from '@/components/Collapse.vue'
// import UserTable from '@/components/UserTable.vue'

export default defineComponent({
  name: 'GroupTableRow',
  components: {
    // UserTable,
    Collapse,
    RenameableLabel
  },
  props: {
    group: {
      type: Object,
      required: true,
    },
  },
  methods: {
    rename(newName: string) {
      // console.log(newName)
      renameGroup(this.group.groupID, newName)
        .then(() => {
          this.$emit('rename', newName)
        }).catch(err => {
            console.log('renameGroup', err)
        })
    },
    leaveHandler() {
      leaveGroup(this.group.groupID)
        .then(() => {
          alert('退出成功')
          this.$emit('delete')
        }).catch(err => {
            console.log('leaveGroup', err)
        })
    }
  },
  computed: {
    bsTarget() {
      return `group${this.group.groupID}`
    },
  }
})
</script>

<style scoped>

</style>
