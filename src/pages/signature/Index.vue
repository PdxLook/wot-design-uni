<!--
 * @Author: 810505339
 * @Date: 2025-02-11 21:17:21
 * @LastEditors: 810505339
<<<<<<< HEAD
 * @LastEditTime: 2025-02-14 12:22:03
=======
 * @LastEditTime: 2025-02-15 21:38:52
>>>>>>> 4c29deae524fe910351cc9a131067fb6124891b7
 * @FilePath: \wot-design-uni\src\pages\signature\Index.vue
 * 记得注释
-->
<template>
  <page-wraper>
    <demo-block title="基础用法">
      <wd-signature @confirm="confirm" @clear="clear" :export-scale="2" />
      <wd-img v-if="img.tempFilePath" mode="widthFix" width="100%" :src="img.tempFilePath" />
    </demo-block>
    <demo-block title="开启历史记录">
      <wd-signature :history="true" background-color="lightgray" />
    </demo-block>
    <demo-block title="自定义画笔颜色">
      <wd-signature pen-color="red" />
    </demo-block>
    <demo-block title="自定义画笔宽度">
      <wd-signature :line-width="6" />
    </demo-block>
    <demo-block title="自定义背景颜色">
      <wd-signature background-color="lightgray" />
    </demo-block>
    <demo-block title="自定义插槽">
      <wd-signature :disabled="disabled" :history="true" :step="3">
        <template #footer="{ clear, confirm, currentStep, restore, revoke, historyList }">
          <wd-button block @click="changeDisabled" v-if="disabled">开始签名</wd-button>
          <block v-if="!disabled">
            <wd-button size="small" plain @click="revoke()" :disabled="currentStep <= 0">撤回三步</wd-button>
            <wd-button size="small" plain @click="restore()" :disabled="!(currentStep < historyList.length)">恢复三步</wd-button>
            <wd-button size="small" plain @click="clear">清除</wd-button>
            <wd-button size="small" style="margin-left: 4px" @click="confirm">确定</wd-button>
          </block>
        </template>
      </wd-signature>
    </demo-block>
  </page-wraper>
</template>

<script lang="ts" setup>
import type { SignatureResult } from '@/uni_modules/wot-design-uni/components/wd-signature/types'
import { ref } from 'vue'

const img = ref<Partial<SignatureResult>>({})

const disabled = ref(true)

function confirm(result: SignatureResult) {
  img.value = result
}

function clear() {
  img.value = {}
}

function changeDisabled() {
  disabled.value = false
}
</script>
