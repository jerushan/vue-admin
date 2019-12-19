<template>
  <div>
    <el-row :gutter="15">
      <el-col :md="24">
        <el-card class="box-card m-b">
          <div slot="header">Basic usage</div>
          <el-radio class="radio m-b" v-model="radio" label="1">optionA</el-radio>
          <el-radio class="radio m-b" v-model="radio" label="2">optionB</el-radio>
            <el-input placeholder="Please input" v-model="input" class="m-b"></el-input>
            <el-input placeholder="Please input" v-model="input" disabled class="m-b"></el-input>
            
            <el-input placeholder="Please input" v-model="input" size="large" class="m-b"></el-input>
            <el-input placeholder="Please input" v-model="input" class="m-b"></el-input>
            <el-input placeholder="Please input" v-model="input" size="small" class="m-b"></el-input>
            <el-input placeholder="Please input" v-model="input" size="mini"></el-input>
        </el-card>
      </el-col>
    </el-row>
  </div>
</template>

<script>
  export default {
    data() {
      return {
        radio: '1',
        radio2: 2,
        options2: [{ label: '1', text: 'optionA' }, { label: '2', text: 'optionB', disabled: true }, { label: '3', text: 'optionC' }]
      }
    },
    methods: {
      onChange() {
        this.$message.info(this.radio2)
      }
    }
  }
</script>