<template>
  <PracticeTable v-slot:default="practice" :practices="practices">
    <GroupTable :practice-id="practice.practiceId" />
<!--    <ActivityTable :practice-id="practice.practiceId" :practice-ended="practice.practiceEnded"/>-->
  </PracticeTable>
</template>

<script lang="ts">
import {defineComponent} from 'vue'
import PracticeTable from '@/components/PracticeTable.vue'
import GroupTable from '@/components/GroupTable.vue'
import {getAllPractice} from '@/services/practice'
import {isLoggedIn} from '@/services/user'
import {useRouter} from 'vue-router'

export default defineComponent({
  name: 'DiscoveryView',
  components: {GroupTable, PracticeTable},
  data() {
    return {
      practices: [],
    }
  },
  methods: {
    refresh() {
      this.practices = []
      getAllPractice().then(res => {
        console.log(res.data)
        this.practices = res.data
      })
    },
  },
  setup() {
    if (!isLoggedIn())
      useRouter().push('/login')
  },
  mounted() {
    this.refresh()
  }
})
</script>

<style scoped>

</style>
