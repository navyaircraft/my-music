<template>
  <draggable v-model="list" @update="datadragEnd" :options="{animation:200}">
    <div class="drag-item" v-for="(item,i) in list" :key="i">
        <el-row>
            <el-col class="line" :span="6">&nbsp;{{item.name}}</el-col>
<!--            <el-col class="line" :span="8">-->
<!--                <el-switch-->
<!--                   v-model="item.is_show"-->
<!--                   active-color="#13ce66"-->
<!--                   @change="lockChange(item)"-->
<!--                   :active-value="1"-->
<!--                   :inactive-value="0"-->
<!--                ></el-switch>-->
<!--            </el-col>-->
            <el-col :span="8">
                <el-button type="text" size="mini" @click="log()">编辑</el-button>
                <el-button type="text" size="mini" @click="sort()">排序</el-button>
                <el-button type="text" size="mini" @click="save()">保存</el-button>
                <el-button type="text" size="mini" @click="diff()">差异</el-button>
<!--                <el-button-->
<!--                   v-if="item.is_system != 1"-->
<!--                   type="text"-->
<!--                   size="mini"-->
<!--                   @click="deleCode(item)"-->
<!--                >删除</el-button>-->
            </el-col>
        </el-row>
    </div>
  </draggable>
</template>
<script src="https://unpkg.com/axios/dist/axios.min.js"></script>
<script>
// import vuedraggable from 'vuedraggable';
import draggable from 'vuedraggable'
export default {
  name: 'HelloWorld',
  // components: {vuedraggable},
  components: { draggable },
  props: {
  },
  data() {
    return {
        // list: [1,2,34,4,54,5]
        list: [
            {'name':'我','dict_order':'1'},
            {'name':'是','dict_order':'2'},
            {'name':'中','dict_order':'3'},
            {'name':'data1:','dict_order':'4'},
            {'name':'人','dict_order':'5'},
            {'name':'国','dict_order':'6'}
        ],
        oldList:{},
        diffList:[],
    }
  },
  updated() {
    for (let i=0; i < this.list.length; i++) {
     // const elem = someArray[index];
     this.list[i].dict_order = i;
     console.log("name->"+this.list[i].name,"dict_order->"+this.list[i].dict_order);
    }

  },
  methods: {
      sort(){
          this.oldList = JSON.stringify(this.list);
          console.log(this.oldList)
      },
      save(){
          let oldData = JSON.parse(this.oldList);
          this.diffList=[];
          for(let i = 0;i<this.list.length;i++){
              console.log("name",this.list[i].name,oldData[i].name,this.list[i].name!=oldData[i].name)
              if((this.list[i].name!=oldData[i].name)
                  ||(this.list[i].dict_order!=oldData[i].dict_order)){
                  this.diffList.push(this.list[i])
              }
          }
      },
      diff(){
          for(let i = 0;i<this.diffList.length;i++){
              console.log("name->"+this.diffList[i].name,"dict_order->"+this.diffList[i].dict_order);
          }
      },
      log(){
          for (let i=0; i < this.list.length; i++) {
              console.log("name->"+this.list[i].name,"dict_order->"+this.list[i].dict_order);
          }
      },
      showEditCode(){
          console.log(this.list);
      },
      async datadragEnd(evt) {
       evt.preventDefault();
       // console.log('拖动前的索引 :' + evt.oldIndex)
       // console.log('拖动后的索引 :' + evt.newIndex)
       // 遍历数组,将索引值赋值到对应的sort_order上面,完成排序
       let arr = this.list;
       let newArr = await arr.map((item, i) => {
         return {
             dict_order: i,
             name: item.name
         };
       });
       // const res = await this.$axios.post(`customer/save_order`, {
       //   list: newArr
       // });
       // // console.log(res)
       // const { error, message } = res.data;
       // if (error == 0) {
       //   this.$message.success(message);
       // }
     },
  }
}
</script>
<style scoped>
.wrapper {
  display: flex;
  justify-content: center;
  width: 100%;
}
.item{
  width: 300px;
  height: 50px;
  background-color: #42b983;
  color: #ffffff;
}
</style>
