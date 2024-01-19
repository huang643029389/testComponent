<template>
    <div class="el-transfer-panel">
      <p class="el-transfer-panel__header">
        <el-checkbox
          v-model="allChecked"
          @change="handleAllCheckedChange"
          :indeterminate="isIndeterminate">
          {{ title }}
          <span>{{ checkedSummary }}</span>
        </el-checkbox>
      </p>
      
      <div :class="['el-transfer-panel__body', hasFooter ? 'is-with-footer' : '']">
        <slot name="aaa"></slot>
        <el-input
          class="el-transfer-panel__filter"
          v-model="query"
          size="small"
          :placeholder="placeholder"
          @mouseenter.native="inputHover = true"
          @mouseleave.native="inputHover = false"
          v-if="filterable">
          <i slot="prefix"
            :class="['el-input__icon', 'el-icon-' + inputIcon]"
            @click="clearQuery"
          ></i>
        </el-input>
        <el-checkbox-group
          v-model="checked"
          v-show="!hasNoMatch && data.length > 0"
          :class="{ 'is-filterable': filterable }"
          class="el-transfer-panel__list">
          <el-checkbox
            class="el-transfer-panel__item"
            :label="item[keyProp]"
            :disabled="item[disabledProp]"
            :key="item[keyProp]"
            v-for="item in filteredData">
            <option-content :option="item"></option-content>
          </el-checkbox>
        </el-checkbox-group>
        <p
          class="el-transfer-panel__empty"
          v-show="hasNoMatch">{{ t('el.transfer.noMatch') }}</p>
        <p
          class="el-transfer-panel__empty"
          v-show="data.length === 0 && !hasNoMatch">{{ t('el.transfer.noData') }}</p>
      </div>
      <p class="el-transfer-panel__footer" v-if="hasFooter">
        <slot></slot>
      </p>
    </div>
</template>
<script>
import TransferPanel from 'element-ui/packages/transfer/src/transfer-panel.vue';
export default {
    extends:TransferPanel
}

</script>