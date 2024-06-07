<template>
  <div>
    <wd-col-picker
      label="选择地址"
      v-model="value"
      :columns="area"
      :column-change="columnChange1"
      @confirm="handleConfirm"
      auto-complete></wd-col-picker>
  </div>
</template>

<script setup lang="ts">
import areaData from '../../utils/area.json'
import { ref, onMounted } from 'vue'
const value = ref<any[]>([])

const area = ref<any[]>(areaData)
const columnChange1 = ({ selectedItem, resolve, finish, index, rowIndex }) => {
  const value = index === -1 ? 86 : selectedItem.value
  if (areaData[value]) {
    resolve(
      Object.keys(areaData[value]).map((key) => {
        return {
          value: key,
          label: areaData[value][key],
        }
      })
    )
  } else {
    finish()
  }
}
function handleConfirm({ value }) {
  console.log(value.value)
}
onMounted(() => {
  console.log('area :>> ', area.value)

  value.value = ['150000', '150100', '150121']
})
</script>

<style scoped></style>
