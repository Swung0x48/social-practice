<template>
  <PracticeTable
      v-slot:default="practice"
      :practices="practices"
      :renameable="false"
      :allow-append="false"
      :show-join="true"
      :privileged="privileged">
    <GroupTable
        :practice-id="practice.practiceId"
        :renameable="false" :privileged="privileged"/>
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
  computed: {
    privileged() {
      return this.$store.getters['user/privileged']
      // return this.$store.state.user.role === 'teacher' || this.$store.state.user.role === 'admin'
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
