<template>
  <div :class="['sidebar', { active: currentView === 'props' }]">
    <BrandLogo />

    <div v-if="currentArea !== area" class="area-name">{{ currentArea.name }}</div>

    <FlexOptions v-if="currentFlex" :flex="currentFlex" />
    <GridOptions v-if="currentGrid" :grid="currentGrid" />
    <a
      class="btn-github"
      target="_blank"
      aria-label="View source on GitHub"
      href="https://github.com/Leniolabs/layoutit-grid"
    >
      <IconGithub />
    </a>
    <VersionLabel />
    <HireUs />
  </div>
</template>

<script setup="props">
export { default as VersionLabel } from './VersionLabel.vue'
export { default as BrandLogo } from './BrandLogo.vue'
export { default as HireUs } from './HireUs.vue'
export { default as IconGithub } from '../icons/IconGithub.vue'
export { default as FlexOptions } from './FlexOptions.vue'
export { default as GridOptions } from './GridOptions.vue'

import { computed } from 'vue'
export { currentArea, currentView } from '../../store.js'

export default {
  props: {
    area: { type: Object, required: true },
  },
}

export const currentGrid = computed(() => currentArea.value.grid)
export const currentFlex = computed(() => currentArea.value.flex)
</script>

<style scoped lang="scss">
.area-name {
  background: #fdd835;
  color: #333;
  padding: 8px 10px;
  top: 0;
  left: 0;
  width: 100%;
  word-break: break-all;
  position: relative;
  border-radius: 2px;
  font-weight: bold;
  &:after {
    content: '';
    bottom: -24px;
    right: 10px;
    position: absolute;
    width: 0;
    height: 0;
    border-style: solid;
    border-width: 12px 10px;
    border-color: #fdd835 transparent transparent;
  }
  &:before {
    content: 'Editing area: ';
    font-weight: normal;
  }
}

.sidebar {
  color: #fff;
  display: grid;
  grid-template-rows: auto 1fr auto;
  overflow: auto;
  padding: 0 10px;
  text-align: left;
  transition: transform 0.2s ease-in;
  user-select: none;
  z-index: 9;
  @media screen and (max-width: 768px) {
    transform: translateX(-15em);
    position: fixed;
    bottom: 0;
    top: 0;
    background: #300748;
    a.brand {
      display: none;
    }
    &.active {
      transform: translateX(0);
    }
  }
}

@media screen and (max-width: 768px) {
  .hire-us,
  .version,
  .btn-undo,
  .btn-redo {
    display: none;
  }
}

.btn-github {
  position: fixed;
  top: 0;
  right: 0;
  z-index: 9;
  opacity: 0.8;
  transition: opacity 0.1s linear;
  &:hover {
    opacity: 0.9;
  }
}
</style>
