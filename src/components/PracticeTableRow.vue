<template>
  <tr>
    <td data-bs-toggle="collapse" :data-bs-target="`#${bsTarget}`">
      {{ practice.practiceID }}
    </td>
    <RenameableLabel
        :name="practice.practiceName"
        @rename="submitRename" />
    <td data-bs-toggle="collapse" :data-bs-target="`#${bsTarget}`">
      {{ practice.startTime }}
    </td>
    <td data-bs-toggle="collapse" :data-bs-target="`#${bsTarget}`">
      {{ practice.endTime }}
    </td>
    <td data-bs-toggle="collapse" :data-bs-target="`#${bsTarget}`">
      {{ practiceStateToString }}
    </td>
    <OperationButtons
        :ended="!practiceEnded"
        @delete="deletePractice"
        @end="endPractice" />
  </tr>
  <Collapse :bsTarget="bsTarget">
    <slot></slot>
  </Collapse>
</template>

<script>
import {deletePractice, endPractice, renamePractice} from '@/services/practice'
import RenameableLabel from '@/components/RenameableLabel'
import OperationButtons from '@/components/OperationButtons'
// import ActivityTable from '@/components/ActivityTable'
import Collapse from '@/components/Collapse'
export default {
  name: 'PracticeTableRow',
  components: {Collapse, OperationButtons, RenameableLabel,
    // ActivityTable
  },
  props: {
    practice: {
      type: Object,
      required: true
    }
  },
  computed: {
    bsTarget() {
      return 'practice' + this.practice.practiceID
    },
    practiceEnded() {
      return this.practice.state === 1
    },
    practiceStateToString() {
      if (this.practice.state === 0)
        return '正在进行'
      else if (this.practice.state === 1)
        return '已结束'
      else
        return this.practice.state
    }
  },
  methods: {
    submitRename(e) {
      // console.log(e)
      renamePractice(this.practice.practiceID, e)
        .then(res => {
          console.log(res.data)
          this.$emit('rename')
          // this.practice.practiceName = this.newName
          // this.cancelRename()
      })
      // this.newName = ''
      // this.renaming = false
    },
    deletePractice() {
      deletePractice(this.practice.practiceID)
          .then(() => {
            alert('删除成功')
            this.$emit('delete')
          })
          .catch(err => {
            alert('删除失败')
            console.log(err)
          })
    },
    endPractice() {
      endPractice(this.practice.practiceID)
          .then(() => {
            alert('结束成功')
            this.$emit('delete')
          })
          .catch(err => {
            alert('结束失败')
            console.log(err)
          })
    }
  }
}
</script>

<style scoped>

</style>
