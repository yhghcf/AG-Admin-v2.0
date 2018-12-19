<template>
  <el-form ref="carFilesForm" :model="form" label-width="80px">
   <div style="padding:40px">
     车牌号码：<el-input v-model="carNumber" style="width: 200px" placeholder="请输入内容"></el-input>&nbsp;
     车辆类型：<el-select v-model="carLists" placeholder="请选择">
                     <el-option
                       v-for="item in carList"
                       :key="item.value"
                       :label="item.label"
                       :value="item.value">
                     </el-option>&nbsp;
              </el-select>
     所属类型：<el-select v-model="carTypes" placeholder="请选择">
                     <el-option
                       v-for="item in carType"
                       :key="item.value"
                       :label="item.label"
                       :value="item.value">
                     </el-option>
                </el-select><br>
     所属公司：<el-input v-model="carCompanies" style="width: 200px;padding-top: 10px" placeholder="请输入内容"></el-input>
               <el-button type="primary"  icon="el-icon-zoom-out"/>
     <div style="display: inline-block;padding-left:388px">
        <el-button type="primary" @click="onSubmit">查询</el-button>
        <el-button>导入</el-button>
     </div>
   </div>
  </el-form>
</template>


<script>
  export default {
    name: 'carFiles',
    data() {
      return {
        carNumber: '',
        carList: [{
          carLists: '选项1',
          label: '车辆'
        }, {
          carLists: '选项2',
          label: '油桶'
        }, {
          carLists: '选项3',
          label: '其它'
        }],
        carType: [{
          carTypes: '选项1',
          label: '自有'
        }, {
          carTypes: '选项2',
          label: '外联挂靠'
        }, {
          carTypes: '选项3',
          label: '外联'
        }],
        carCompanies: ''
      }
    }
  }
</script>
