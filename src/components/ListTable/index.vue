<template>
  <!-- key根据后端唯一值进行替换 -->
  <el-card v-loading="isLoding" shadow="never">
    <!-- 表格 -->
    <div class="table-wrapper">
      <el-table row-key="id" :data="list" style="width: 100%">
        <el-table-column
          v-for="column in columns"
          :key="column.name"
          :prop="column.name"
          :label="column.label"
          :width="column.width"
          align="center"
        >
          <template v-if="column.type === 'button'" #default="scope">
            <div>
              <el-button
                v-for="action in column.actions"
                :key="action.label"
                link
                type="primary"
                size="small"
                @click="action.handler(scope.row)"
              >
                {{ action.label }}
              </el-button>
            </div>
          </template>
        </el-table-column>
      </el-table>
    </div>
    <!-- 分页 -->
    <div class="pager-wrapper" v-if="isPagination">
      <el-pagination
        v-model:current-page="page"
        v-model:page-size="pageSize"
        :page-sizes="[10, 20, 50, 100]"
        :size="'default'"
        :background="true"
        layout="total, sizes, prev, pager, next"
        :total="total"
        @size-change="handleSizeChange"
        @current-change="handleCurrentChange"
      />
    </div>
  </el-card>
</template>

<script setup lang="ts">
import { request } from "@/utils/service"

import { onMounted, ref, watch } from "vue"
const props = defineProps<{
  url: string
  isPagination?: boolean
  columns: Array<{ name: string; label: string }>
}>()

const processObject = (obj) => {
  for (let key in obj) {
    if (Array.isArray(obj[key])) {
      return key
    }
  }
}

const getListApi = (params) => {
  return request({
    url: props.url,
    method: "get",
    params
  })
}

const list = ref()
const page = ref(1)
const pageSize = ref(10)
const total = ref(100)
const isLoding = ref(false)

const handleSizeChange = (val: number) => {
  pageSize.value = val
}
const handleCurrentChange = (val: number) => {
  page.value = val
}

const getTableData = async () => {
  try {
    isLoding.value = true

    const res = await getListApi({
      currentPage: page.value,
      size: pageSize.value,
      username: "",
      phone: ""
    })

    const key = processObject(res.data)

    list.value = res.data[key]
    total.value = res.data.total
  } catch (error) {
    console.error("Error fetching table data:", error)
  } finally {
    isLoding.value = false
  }
}

watch([page, pageSize], ([newPage, newPageSize]) => {
  getTableData()
})

getTableData()
</script>

<style scoped>
.table-wrapper {
  margin-bottom: 20px;
}

.pager-wrapper {
  display: flex;
  justify-content: flex-end;
}
</style>
