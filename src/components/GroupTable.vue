<template>
  <table class="table">
    <thead>
    <tr>
      <th>小组编号</th>
      <th>小组名</th>
      <th>关联的社会实践活动编号</th>
      <th>操作</th>
    </tr>
    </thead>
    <tbody>
      <GroupTableRow v-for="group in groups"
                     :key="group.groupID"
                     :group="group"
                     @delete="refresh"
                     @rename="refresh">
        <UserTable :group-id="group.groupID" />
      </GroupTableRow>
    </tbody>
  </table>
</template>

<script lang="ts">
import {defineComponent, onBeforeMount} from 'vue'
import GroupTableRow from '@/components/GroupTableRow.vue'
import {getAllGroup} from '@/services/group'
import {isLoggedIn} from '@/services/user'
import {useRouter} from 'vue-router'
import UserTable from '@/components/UserTable.vue'

export default defineComponent({
  name: 'GroupTable',
  components: {
    GroupTableRow,
    UserTable
  },
  props: {
    groups: {
      type: Array,
      required: true
    }
  },
  // data() {
  //   return {
  //     groups: []
  //   }
  // },
  methods: {
    refresh() {
      this.$emit('refresh')
    }
    // refresh() {
    //   getAllGroup().then(res => {
    //     this.groups = res.data
    //   })
    // }
  },
  // setup() {
  //   onBeforeMount(() => {
  //     if (!isLoggedIn())
  //       useRouter().push('/login')
  //   })
  // },
  // mounted() {
  //   getAllGroup()
  //     .then(res => {
  //       console.log(res.data)
  //       this.$data.groups = res.data
  //     })
  // }
})
</script>

<style scoped>

</style>
