<template>
  <div class="app-container">
    <ListTable :url="'table'" :isPagination="true" :columns="columns" />
  </div>
</template>

<script setup lang="ts">
import ListTable from "@/components/ListTable/index.vue"

const handleClick = (record) => {
  console.log("record", "是数据值")
}

const columns = [
  {
    name: "username",
    label: "用户名"
  },
  {
    name: "email",
    label: "邮箱"
  },
  {
    name: "actions",
    label: "操作",
    type: "button",
    actions: [
      {
        label: "详情",
        handler: handleClick
      },
      {
        label: "编辑",
        handler: () => {}
      }
    ]
  }
]
</script>

<style scoped></style>
