<template>
  <div class="hello">
    <Button type="success" @click="outExe">导出Excel</Button>
  </div>
</template>

<script>
export default {
  name: 'HelloWorld',
  data () {
    return {
      msg: 'Welcome to Your Vue.js App'
    }
  },
  methods: {
     outExe() {
                this.$confirm('此操作将导出excel文件, 是否继续?', '提示', {
                    confirmButtonText: '确定',
                    cancelButtonText: '取消',
                    type: 'warning'
                }).then(() => {
                    this.excelData = [
             {id: 1, title: 2, author: 3, pageviews: 4, display_time: 5},
             {id: 6, title: 7, author: 8, pageviews: 9, display_time: 10},
             {id: 11, title: 12, author: 13, pageviews: 14, display_time: 15},
            ]; //你要导出的数据list。
                    this.export2Excel()
                }).catch(() => {
                
                });
            },
            export2Excel() {
        var that= this;
        require.ensure([], () => {
          const { export_json_to_excel } = require('../assets/vendor/Export2Excel');
          const tHeader =
            [
            '编号', '标题', '作者','回顾', '时间'    
            ];
          const filterVal =
            ['id', 'title','author','pageviews','display_time'];  
           const list = that.excelData;
                   const data = that.formatJson(filterVal, list);    
          export_json_to_excel(tHeader, data, '**账单报表');
        })
      },
      formatJson(filterVal, jsonData) {
        return jsonData.map(v => filterVal.map(j => v[j]))
    }
    },
    computed:{
 
    },
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>

</style>
