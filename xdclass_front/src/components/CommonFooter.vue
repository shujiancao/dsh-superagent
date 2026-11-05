<template>
  <nav class="common-footer" aria-label="主导航">
    <div class="common-footer__bar">
      <cube-tab-bar :value="$route.path" @click="handleTabClick">
        <cube-tab
          v-for="item in tabs"
          :key="item.path"
          :icon="item.icon"
          :label="item.label"
          :value="item.path"
          role="link"
          :aria-current="isActive(item.path) ? 'page' : null"
          tabindex="0"
          @keydown.native.enter="handleTabClick(item.path)"
          @keydown.native.space.prevent="handleTabClick(item.path)"
        ></cube-tab>
      </cube-tab-bar>
    </div>
  </nav>
</template>

<script>
export default {
  name: "CommonFooter",
  computed: {
    tabs() {
      return this.$router.options.routes
        .filter(route => route.meta && route.meta.tab)
        .map(route => ({
          label: route.meta.tab.label,
          icon: route.meta.tab.icon,
          path: route.path
        }));
    }
  },
  methods: {
    isActive(path) {
      return path === this.$route.path;
    },
    handleTabClick(path) {
      if (!this.isActive(path)) {
        this.$router.push(path);
      }
    }
  }
};
</script>

<style lang="scss" scoped>
@import "../assets/styles/variables";

$footer-height: 48px;
$footer-gap: 12px;

// 占位：fixed 底栏不占文档流，为页面底部预留「栏高 + 间距」，避免内容被遮挡
.common-footer {
  height: calc(#{$footer-height} + #{$footer-gap});
  height: calc(#{$footer-height} + #{$footer-gap} + constant(safe-area-inset-bottom));
  height: calc(#{$footer-height} + #{$footer-gap} + env(safe-area-inset-bottom, 0px));
}

.common-footer__bar {
  position: fixed;
  right: 0;
  bottom: 0;
  left: 0;
  z-index: 100;
  box-sizing: content-box;
  height: $footer-height;
  padding-bottom: constant(safe-area-inset-bottom);
  padding-bottom: env(safe-area-inset-bottom, 0px);
  background-color: #fff;
  border-top: 1px solid rgba(0, 0, 0, 0.1);
}

.common-footer__bar .cube-tab-bar {
  height: 100%;
}

.cube-tab {
  cursor: pointer;
}

.cube-tab_active {
  color: $brand-green;
}

.cube-tab:focus-visible {
  outline: 2px solid $brand-green;
  outline-offset: -2px;
}
</style>
