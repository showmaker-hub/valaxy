<script lang="ts" setup>
/**
 * @file 生成首页标语动画
 * @author YunYouJun <me@yunyoujun.cn>
 * @description https://github.com/YunYouJun/hexo-theme-yun
 */

import { CSSProperties, computed } from 'vue'
import { random } from 'valaxy'
import { useThemeConfig } from '../composables'

const themeConfig = useThemeConfig()

const chars = computed(() => {
  const arr = []
  for (let i = 0; i < themeConfig.value.banner.title.length; i++) {
    const rn = random(1.5, 3.5)
    arr.push(rn)
  }
  return arr
})
// height of top/bottom line
const lineH = computed(() => chars.value.reduce((a, b) => a + b, 0) / 2)

const lintStyle = computed(() => (
  {
    '--banner-line-height': `calc(50vh - ${lineH.value}rem)`,
  } as CSSProperties
))
</script>

<template>
  <div id="banner">
    <div class="banner-line vertical-line-top" :style="lintStyle" />
    <div class="banner-char-container">
      <div v-for="c, i in themeConfig.banner.title" :key="i" class="char-box">
        <span
          :class="[i % 2 !== 0 ? 'char-right' : 'char-left']" :style="{
            '--banner-char-size': `${chars[i]}rem`,
          } as CSSProperties"
        >
          <span class="char">
            {{ c }}
          </span>
        </span>
      </div>
    </div>
    <div class="banner-line vertical-line-bottom" :style="lintStyle" />
  </div>

  <YunGoDown />
</template>

<style lang="scss">
:root {
  // banner
  --banner-line-color: black;
  --banner-char-color: black;
  --banner-char-bg-color: rgba(white, 0.5);
  --banner-char-hover-color: white;
}

.dark {
  // banner
  --banner-line-color: white;
  --banner-char-color: white;
  --banner-char-bg-color: rgba(black, 0.5);
  --banner-char-hover-color: black;
}
</style>
