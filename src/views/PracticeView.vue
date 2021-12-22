<template>
  <PracticeTable
      v-slot:default="practice"
      :practices="practices"
      @refresh="refresh">
<!--    {{ slotProp }}-->
    <ActivityTable :practice-id="practice.practiceId" :practice-ended="practice.practiceEnded"/>
  </PracticeTable>
</template>

<script>
import {defineComponent} from 'vue'
import PracticeTable from '@/components/PracticeTable'
import ActivityTable from '@/components/ActivityTable'
import {getMyPractice} from '@/services/practice'
import {isLoggedIn} from '@/services/user'
import {useRouter} from 'vue-router'

export default defineComponent({
  practiceName: 'PracticeView',
  components: {
    PracticeTable,
    ActivityTable
  },
  data() {
    return {
      practices: [],
    }
  },
  methods: {
    refresh() {
      this.practices = []
      getMyPractice().then(res => {
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
    // getMyPractice().then(res => {
    //   console.log(res.data)
    //   this.practices = res.data
    // })
  }
})
</script>

<style scoped>

</style>
