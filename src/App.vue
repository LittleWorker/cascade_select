<template>
  <div id="app">
    <cascade :cascadeList="cascadeList"></cascade> 
  </div>
</template>

<script>
import cascade from './components/cascade.vue';
export default {
  name: 'app',
  data () {
    return {
      cascadeList:[
        {name:'中国',
         value:['北京','上海','深圳']},
        {name:'美国',
         value:['纽约','洛杉矶','华盛顿']},
        {name:'英国',
         value:['伦敦','伯明翰','曼切斯特']}
      ]  
    }
  },
  created () {
    let that = this;
    //二级下拉框选择事件
    this.$bus.on('level2Changed',function(levelIndex){ 
      let index1 = levelIndex.index1,
          index2 = levelIndex.index2;
      console.log(that.cascadeList[index1].name+"  "+that.cascadeList[index1].value[index2]);
    });
  },
  components: {
    cascade
  }
}
</script>

<style>
#app {
  font-family: 'Avenir', Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
</style>
