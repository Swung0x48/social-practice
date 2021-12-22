<template>
  <GroupTable
      @refresh="refresh"
      :groups="groups"
      :renameable="privileged"
      :privileged="privileged"/>
</template>

<script lang="ts">
import {defineComponent, onBeforeMount} from 'vue'
import GroupTable from '@/components/GroupTable.vue'
import {getAllGroup} from '@/services/group'
import {isLoggedIn} from '@/services/user'
import {useRouter} from 'vue-router'

export default defineComponent({
  practiceName: 'GroupView',
  components: {GroupTable},
  data() {
    return {
      groups: []
    }
  },
  computed: {
    privileged() {
      return this.$store.getters['user/privileged']
    }
  },
  methods: {
    refresh() {
      getAllGroup().then(res => {
        this.groups = res.data
      })
    }
  },
  setup() {
    onBeforeMount(() => {
      if (!isLoggedIn())
        useRouter().push('/login')
    })
  },
  mounted() {
    getAllGroup()
        .then(res => {
          console.log(res.data)
          this.$data.groups = res.data
        })
  }
})
</script>

<style scoped>

</style>
