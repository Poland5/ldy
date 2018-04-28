<template>
  <div class="hello">
    <div style="margin-bottom:20px;">
      <el-select v-model="value" placeholder="请选择" @change="ldyChange(value)">
        <el-option
          v-for="item in ldyOptions"
          :key="item.value"
          :label="item.label"
          :value="item.value">
        </el-option>
      </el-select>
      <el-select v-model="value1" placeholder="请选择" @change="typeChange(value1)">
      <el-option
        v-for="item in typeOptions"
        :key="item.value1"
        :label="item.label"
        :value="item.value1">
      </el-option>
    </el-select>
    </div>
  </div>
</template>
<script>
export default {
  data () {
    return {
      ldyOptions: [{
          value: 'lsqy',
          label: '猎杀契约'
        }, {
          value: 'mhtj',
          label: '梦幻天剑'
        }, {
          value: 'wzqst',
          label: '王者骑士团'
        }, {
          value: 'hlw',
          label: '葫芦娃'
        }, {
          value: 'pxzr',
          label: '破晓之刃'
        }, {
          value: 'lzhx',
          label: '龙之幻想'
        }, {
          value: 'smqy',
          label: '宿命契约'
        }, {
          value: 'jpmx',
          label: '极品萌仙'
        }],
        value: '',
      typeOptions:[{
        value1:'ios',
        label:'苹果'
      },{
        value1:'and',
        label:'安卓'
      }],
      value1:''
    };
  },
  methods:{
    ldyChange(row){
      this.$emit('ldyTitle',row)
    },
    typeChange(row){
      this.$emit('typeTitle',row)
    }
  }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>

</style>
