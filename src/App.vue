<template>
  <div id="app">
    <el-input v-model="query"></el-input>
    <!-- <HelloWorld msg="Welcome to Your Vue.js App"/> -->
    <el-transfer filterable v-model="value" :data="data"></el-transfer>
    <my-transfer filterable v-model="value" :data="data">
      <template slot="left-aaa">
        <el-select v-model="selectform">
          <el-option value="1" label="1"></el-option>
          <el-option value="2" label="2"></el-option>
          <el-option value="2" label="2"></el-option>
        </el-select>
      </template>
    </my-transfer>
  </div>
</template>

<script>
import MyTransfer from './components/my-transfer/TransferIndex.vue'

export default {
  name: 'App',
  components: {
    MyTransfer
  },
  data(){
    const generateData = () => {
        const data = [];
        for (let i = 1; i <= 15; i++) {
          data.push({
            key: i,
            label: `备选项 ${ i }`,
            disabled: i % 4 === 0
          });
        }
        return data;
      };
    return {
      query: '',
      selectform: '',
      data: generateData(),
        value: [1, 4]
    }
  }
}
</script>

<style>

</style>
