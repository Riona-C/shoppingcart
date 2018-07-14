<template>
  <div id="shop" v-if="list.length">
    <table>
      <thead>
        <tr>
          <th></th>
          <th>商品名称</th>
          <th>商品单价</th>
          <th>购买数量</th>
          <th>操作</th>
        </tr>
      </thead>
      <tbody>
        <tr v-for="(item,index) in list">
          <td>{{index+1}}</td>
          <td>{{item.name}}</td>
          <td>{{item.price}}</td>
          <td>
            <button @click="handleReduce(index)">-</button>
            {{item.count}}
            <button @click="handleAdd(index)">+</button>
          </td>
          <td>
            <button @click="handleRemove(index)">删除</button>
          </td>
        </tr>
      </tbody>
      <div>总价：￥{{totalPrice}}</div>
    </table>
  </div>
  <div v-else>购物车为空</div>
</template>

<script>
    export default {
        name: "index",
        data (){
          return{
            list:[
              {
                id:1,
                name:'苹果',
                price:30,
                count:1
              },
              {
                id:2,
                name:'香蕉',
                price:100,
                count:2
              },
              {
                id:3,
                name:'荔枝',
                price:80,
                count:1
              }
            ]
          }
        },
        computed:{
          totalPrice:function(){   //计算总价
            var total = 0;
            for(var i = 0;i < this.list.length;i++){
              var item = this.list[i];
              total += item.price * item.count;
            }
            //返回总价  并加千分符
            return total.toString().replace(/\B(?=(\d{3})+$)/g,',');
          }
        },
        methods:{
          handleReduce:function(index){  //减少数量
            if(this.list[index].count === 1) return;
            this.list[index].count--;
          },
          handleAdd:function(index){    //增加数量
            this.list[index].count++;
          },
          handleRemove:function(index){      //删除当前产品
            this.list.splice(index,1);
          }
        },

    }
</script>

<style scoped>
  table{
    border:1px solid #e9e9e9;
    border-collapse:collapse;
    border-spacing:0;
    empty-cells:show;
  }
  th,td{
    padding:8px 8px;
    border:1px solid #e9e9e9;
    text-align:left;
  }
  th{
    background: #f7f7f7;
    color:#5c6b77;
    font-weight:600;
    white-space:nowrap;
  }
</style>
