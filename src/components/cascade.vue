<template>
    <div class="cascade">
        <select name="level1" id="level1" @change="level1Changed($event)" >
            <option v-for="item in list1" :key="item.index" :value="item">{{item}}</option>
        </select>
        <select name="level2" id="level2" @change="level2Changed($event)">
            <option v-for="item in list2" :key="item.index" :value="item">{{item}}</option>
        </select>
    </div>
</template>

<script>
 export default {
    name:'cascade',
    props:{
        cascadeList:Array
    },
    data () {
        return {
            level1_index:0
        }
    },
    components: {

    },
    methods: {
      level1Changed(event){
          this.level1_index = event.target.selectedIndex;
          //触发二级下拉框强制选择第1条数据
          document.getElementById('level2')[0].selected =true;
          let levelIndex={
              index1:this.level1_index,
              index2:0
          }
          this.$bus.emit('level2Changed',levelIndex);
      },
      level2Changed(event){
          let levelIndex={
              index1:this.level1_index,
              index2:event.target.selectedIndex
          }
          this.$bus.emit('level2Changed',levelIndex);
      }    
    },
    computed:{
        list1:function(){
            let temp_list=[];
            for(let i in this.cascadeList){
                temp_list.push(this.cascadeList[i].name);
            }
            return temp_list;
        },
        list2:function(){
            return this.cascadeList[this.level1_index].value;
        }
    },
    mounted () {
        //触发初始化选择事件
        let levelIndex={
              index1:0,
              index2:0
          }
        this.$bus.emit('level2Changed',levelIndex);
    }
 }
</script>

<style>
    .cascade{
        position: relative;
    }
    select{
       width:auto;
       min-width:100px;
       height: 36px;
       font-size: 24px;
       line-height: 36px;
       text-align: center; 
       padding-left:8px; 
    }
</style>
