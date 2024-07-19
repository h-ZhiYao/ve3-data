<script lang="ts" setup>
import { ref, computed } from "vue"
import { ElMessage } from "element-plus"
import { Bell } from "@element-plus/icons-vue"
</script>

<template>
  <div class="notify">
    <el-dropdown class="right-menu-item">
      <el-badge :value="50" :max="99" :hidden="true">
        <el-icon :size="20">
          <Bell />
        </el-icon>
      </el-badge>
      <template #dropdown>
        <el-dropdown-menu>
          <el-dropdown-item>
            <span style="display: block">全部消息</span>
          </el-dropdown-item>
          <el-dropdown-item>
            <span style="display: block">产品消息</span>
          </el-dropdown-item>
          <el-dropdown-item>
            <span style="display: block">安全消息</span>
          </el-dropdown-item>
          <el-dropdown-item>
            <span style="display: block">服务消息</span>
          </el-dropdown-item>
        </el-dropdown-menu>
      </template>
    </el-dropdown>
  </div>
</template>

<style lang="scss" scoped>
.notify {
  margin-right: 10px;
}

.notify-history {
  text-align: center;
  padding-top: 12px;
  border-top: 1px solid var(--el-border-color);
}
</style>
