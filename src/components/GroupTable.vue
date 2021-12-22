<template>
  <table class="table table-striped">
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
                     @rename="refresh"
                     :privileged="privileged">
        <UserTable :group-id="group.groupID" />
      </GroupTableRow>
      <GroupTableRow v-for="group in groupsData"
                     :key="group.groupID"
                     :group="group"
                     @delete="refresh"
                     @rename="refresh"
                     :privileged="privileged">
        <UserTable :group-id="group.groupID" />
      </GroupTableRow>
    </tbody>
  </table>
</template>

<script lang="ts">
import {defineComponent, onBeforeMount} from 'vue'
import GroupTableRow from '@/components/GroupTableRow.vue'
import {getAllGroup, getGroupByPracticeID} from '@/services/group'
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
      default: () => []
    },
    practiceId: {
      type: Number,
      default: -1
    },
    privileged: {
      type: Boolean,
      required: true
    }
  },
  data() {
    return {
      groupsData: []
    }
  },
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
  setup() {
    onBeforeMount(() => {
      if (!isLoggedIn())
        useRouter().push('/login')
    })
  },
  mounted() {
    getGroupByPracticeID(this.practiceId)
      .then(res => {
        console.log(res.data)
        this.$data.groupsData = res.data
      })
  }
})
</script>

<style scoped>

</style>
