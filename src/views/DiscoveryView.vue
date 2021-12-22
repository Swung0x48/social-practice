<template>
  <PracticeTable v-slot:default="practice">
    <GroupTable />
<!--    <ActivityTable :practice-id="practice.practiceId" :practice-ended="practice.practiceEnded"/>-->
  </PracticeTable>
</template>

<script lang="ts">
import {defineComponent} from 'vue'
import PracticeTable from '@/components/PracticeTable'
import GroupTable from '@/components/GroupTable'
import { getGroupByPracticeID } from '@/services/group'

export default defineComponent({
  name: 'DiscoveryView',
  components: {GroupTable, PracticeTable},
  data() {
    return {
      groups: []
    }
  },
  methods: {
    getGroups(practiceId: number) {
      getGroupByPracticeID(practiceId)
        .then(res => {
          this.groups = res.data
        })
    }
  }
})
</script>

<style scoped>

</style>
