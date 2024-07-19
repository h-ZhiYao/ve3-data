<script lang="ts" setup>
import { useLayoutMode } from "@/hooks/useLayoutMode"

const VITE_APP_TITLE = import.meta.env.VITE_APP_TITLE

interface Props {
  collapse?: boolean
}

const props = withDefaults(defineProps<Props>(), {
  collapse: true
})

const { isLeft, isTop } = useLayoutMode()
</script>

<template>
  <div class="layout-logo-container" :class="{ collapse: props.collapse, 'layout-mode-top': isTop }">
    <transition name="layout-logo-fade">
      <router-link class="layout-logo-content">
        <img
          src="http://144.48.83.77:9002/xh_admin/images/%E7%B3%BB%E7%BB%9F%E6%A1%86%E6%9E%B6/u38.svg"
          class="layout-logo-text"
          alt=""
        />
        <div class="layout-text">{{ VITE_APP_TITLE }}</div>
      </router-link>
    </transition>
  </div>
</template>

<style lang="scss" scoped>
.layout-logo-container {
  position: relative;
  width: 100%;
  height: var(--v3-header-height);
  line-height: var(--v3-header-height);
  text-align: center;
  overflow: hidden;
  .layout-logo {
    display: none;
  }
  .layout-logo-text {
    width: 20%;
    margin-right: 10px;
  }
  .layout-logo-content {
    display: flex;
    justify-content: center;
    align-items: center;
  }
  .layout-text {
    font-size: 20px;
    color: #fcfcfc;
  }
}

.layout-mode-top {
  height: var(--v3-navigationbar-height);
  line-height: var(--v3-navigationbar-height);
}

.collapse {
  .layout-logo {
    width: 32px;
    height: 32px;
    vertical-align: middle;
    display: inline-block;
  }
  .layout-logo-text {
    display: none;
  }
}
</style>
