<template>
  <PracticeTable v-slot:default="practice">
    <GroupTable :practice-id="practice.practiceId" />
<!--    <ActivityTable :practice-id="practice.practiceId" :practice-ended="practice.practiceEnded"/>-->
  </PracticeTable>
</template>

<script lang="ts">
import {defineComponent} from 'vue'
import PracticeTable from '@/components/PracticeTable.vue'
import GroupTable from '@/components/GroupTable.vue'

export default defineComponent({
  name: 'DiscoveryView',
  components: {GroupTable, PracticeTable},
})
</script>

<style scoped>

</style>
