<template>
  <PracticeTable v-slot:default="practice">
<!--    {{ slotProp }}-->
    <ActivityTable :practice-id="practice.practiceId" :practice-ended="practice.practiceEnded"/>
  </PracticeTable>
</template>

<script>
import {defineComponent} from 'vue'
import PracticeTable from '@/components/PracticeTable'
import ActivityTable from '@/components/ActivityTable'

export default defineComponent({
  practiceName: 'PracticeView',
  components: {
    PracticeTable,
    ActivityTable
  }
})
</script>

<style scoped>

</style>
