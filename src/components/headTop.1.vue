<template>
  <div class="hello">
    <div style="margin-bottom:20px;">
      <el-radio-group v-model="radio1">
        <el-radio-button label="猎杀契约"></el-radio-button> 
        <el-radio-button label="梦幻天剑"></el-radio-button>
        <el-radio-button label="王者骑士团"></el-radio-button> 
        <el-radio-button label="葫芦娃"></el-radio-button>
        <el-radio-button label="破晓之刃"></el-radio-button> 
        <el-radio-button label="龙之幻想"></el-radio-button> 
        <el-radio-button label="宿命契约"></el-radio-button> 
        <el-radio-button label="极品萌仙"></el-radio-button> 
      </el-radio-group>
    </div>
    <div>
      <el-radio-group v-model="radio2">
        <el-radio-button label="苹果"></el-radio-button>
        <el-radio-button label="安卓"></el-radio-button>
      </el-radio-group>
    </div>
  </div>
</template>

<script>
export default {
  data () {
    return {
      radio1: '上海',
      radio2: '上海',
    };
  }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>

</style>
