<template>
  <div>
    <head-top @ldyTitle='listen_ldy' @typeTitle='listen_type'></head-top>
    <el-table
      :data="tableData"
      stripe
      style="width: 800px; margin:0 auto; text-align:left">
      <el-table-column prop="ldy" label="落地页名称" width="180"></el-table-column>
      <el-table-column prop="category" label="手机类型" width="180"></el-table-column>
      <el-table-column prop="url" label="地址"></el-table-column>
      <el-table-column label="操作" width="80">
        <template slot-scope="scope">
          <el-button @click="openUrl(scope.row)" type="text" size="small">
            链接
          </el-button>
        </template>
      </el-table-column>
    </el-table>
  </div>
</template>

<script>
import $ from 'jquery'
import headTop from '@/components/headTop'

export default {
  name: 'App',
  data() {
    return {
      products:[],
      tmpProducts:[],
      tableData: [],
      ldyUrl:'',
      ldyTitle:'',
      typeTitle:'',
      conditions: new Array(2)
    }
  },
  components: {
    headTop
  },
  methods: {
    async getList(){
      let res;
      if(this.tmpProducts.length){
        res = this.tmpProducts;
      }else{
        res = this.products;
      }
      this.tableData = [];
        if(res){
          res.forEach((item,index) => {
            const tableData = {
              ldy: item.ldy,
              category: item.brand,
              url: `http://tui.zisugame.com/${item.value}`
            };
            this.tableData.push(tableData);
          })
      }else{
        console.log("数据获取失败");
      }
    },
    toFilter(products, condition){
      const ProductFilter = {
        matchFilter: function(products, match){
          if(products.length == 0){
            return products;
          }else{
             return products.filter((item,index) => {
             return item.name.indexOf(match.value) !== -1;
            })
          }
        },
        likeFilter: function(products, like){
          let tmpProducts = [];
          if(like.length == 0){
            tmpProducts = products
          }else{
            tmpProducts = products.filter(item => {
              return item.name.indexOf(like.value) !== -1;
            })
            return tmpProducts;
          }
        }
      }
      this.conditions.forEach((item, index) => {
        const key = item.type;
        if(ProductFilter.hasOwnProperty(key + 'Filter') && typeof ProductFilter[key + 'Filter'] === 'function'){
          products = ProductFilter[key + 'Filter'](products, condition);
        }
       })
      this.tmpProducts = products;
      this.getList();     
    },
    openUrl(row){
      window.location.href = row.url;
    },
    listen_ldy(msg){
      this.ldyTitle = msg;
      let condition = {
        type:'match',
        value:msg
      }
      this.conditions[0] = condition;
      this.toFilter(this.products, this.conditions[0]);
    },
    listen_type(msg){
      this.typeTitle = msg;
      let condition = {
        type:'like', 
        value:msg
      }
      this.conditions[1] = condition;
      this.toFilter(this.products, this.conditions[1]);
    }
  },
  mounted(){
     var that=this;
      $.ajax({
        async : false,
        url : "http://tui.zisugame.com/getList.php",
        type : "GET",
        dataType : "jsonp", // 返回的数据类型，设置为JSONP方式
        jsonp : 'callback', //指定一个查询参数名称来覆盖默认的 jsonp 回调参数名 callback
        jsonpCallback: 'callback', //设置回调函数名
        success:function(data) {
          that.data = data;
        }
      }).then(() =>{
        const res = this.data;
        let products = [];
        res.forEach((item, index) => {
          let num = item.replace(/[^0-9]/ig,"");
          let name = item.split('/')[0];
          let category = /ios/ig.test(item) ? 'ios' : 'and';
          let ldy = '';
          let brand = '';
          switch(name){
            case 'lsqy':
            ldy = '猎杀契约';
            break;
            case 'mhtj':
            ldy = '梦幻天剑';
            break;
            case 'wzqst':
            ldy = '王者骑士团';
            break;
            case 'hlw':
            ldy = '葫芦娃';
            break;
            case 'pxzr':
            ldy = '破晓之刃';
            break;
            case 'lzhx':
            ldy = '龙之幻想';
            break;
            case 'smqy':
            ldy = '宿命契约';
            break;
            case 'jpmx':
            ldy = '极品萌仙';
            break;
          };
          switch(category){
            case 'ios':
            brand = '苹果';
            break;
            case 'and':
            brand = '安卓';
            break;
          }
          let products = {
            key : parseInt(num),
            name : name,
            category :  category,
            value : item,
            ldy : ldy,
            brand : brand
          }
          this.products.push(products);
        })
        this.getList();
      })
  }
}
</script>

<style>

</style>
