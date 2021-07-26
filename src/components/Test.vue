<template>
  <vuedraggable class="wrapper" v-model="list">
    <transition-group>
      <div v-for=" (item,i) in list" :key="i" class="item">
        <p>{{item.name}}</p>
      </div>
    </transition-group>
  </vuedraggable>
</template>
<script src="https://unpkg.com/axios/dist/axios.min.js"></script>
<script>
import vuedraggable from 'vuedraggable';

export default {
  name: 'HelloWorld',
  components: {vuedraggable},
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
      ]
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
 //   getList:{
 //       axios.post('/api/my/list',{
 //       }).then(function(res){
 //           this.list = res;
 //       });
 //   }
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
