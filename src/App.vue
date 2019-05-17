<template>
  <div class="wrap">
    <header>
          <span class="active1">菜单</span>
          <span>评价</span>
          <span>商家</span>
    </header>
    <section>
       <div class="left">
            <ul>
                <li v-for="(item,index) in classify" :key="index" :class="{'active':index == ind}" @click="change(index,item.type)">{{item.title}}                 
                </li>
            </ul>
       </div>
       <div class="right">    
            <my-list v-for="(item1,index1) in list" :key="index1"
              :title="item1.title"
              :price="item1.price"
              :id="item1.id"
              
              :type="item1.type"
              :pic="item1.pic"
            ></my-list>      
       </div>
    </section>
 
  </div>
</template>
<script>
//App.vue----》my.list.vue      my.list.vue--->my.count.vue

import myList from "./components/my-list";
import list from "./js/list.js";//右边商品详情
import classify from './js/classify.js';//左侧列表数据

export default {
  props: {},
  components: {
      myList
  },
  data() {
    return {
      classify:[],
      list:[],
      buyList:[],
      ind:0
    };
  },
 computed: {
        totalPrice() {
            return this.buyList.reduce(
                (prev, cur) => prev + cur.num * cur.price,
                0
            );
        },
        totalCount() {
            return this.buyList.reduce((prev, cur) => prev + cur.num, 0);
        }
  },
  methods: {
        getList(list, type) {
            //筛选数据
            return list.filter(item => item.type == type);
        },
        change(ind, type) {
            //切换
            this.ind = ind;
            this.list = this.getList(list, type);
        }
        // showDialog(){
        //     this.isShow = !this.isShow;
        // }
    },
created() {
        this.classify = classify;
        this.list = this.getList(list, this.classify[0].type);
        console.log(this);
        this.$bus.$on("addCount", (num, id,type) => {
            console.log(num);
            this.list = this.getList(list,type);
            let index = this.list.findIndex(item => item.id == id);
            this.list[index].num = num;
            let ind = this.buyList.findIndex(item => item.id == id);
            if (ind == -1) {
                this.buyList.push(this.list[index]);
            }
            let cur = this.classify.findIndex(item=> item.type == type);
            this.ind = cur;
        });
    },
  mounted() {
      
  }
};
</script>
<style>
* {
  list-style: none;
  margin: 0;
  padding: 0;
}
html,
body,
.wrap {
  width: 100%;
  height: 100%;
}
.wrap {
  /* width: 100%;
  height: 100%; */
  display: flex;
  flex-direction: column;
}
header {
      width: 100%;
      height: 50px;
      display: flex;
      align-items:center;
      box-sizing:border-box;
      border-bottom:1px solid #ccc;
}
header span{
    flex:1;
    text-align: center;
    height: 50px;
    line-height: 50px;
    font-size: 18px;
}
section{
    width: 100%;
    flex: 1;
    /* overflow: scroll; */
    display: flex;
}
.left{
    width:110px;
    height: 100%;    
}
.left li{
   width: 100%;
   height: 75px;
   line-height: 75px;
   text-align: center;
   font-size: 18px;
   /* border-bottom: 1px solid #ccc; */
}
.active{
  color: brown;
  font-size: 18px;
  font-weight: 800;
}
.active1{
   color: #000;
  font-size: 19px;
  font-weight: 800;
  border-bottom: 1px solid  orange;
}
.right{
    height: 100%;
    flex: 1;
    overflow: scroll; 
    overflow: hidden;

}
footer{
  width: 100%;
  height: 60px;
  background: wheat;
  display: flex;
}
.bot{
  width: 70%;
  height: 60px;
  background: #000;
}
.bot img{
    width: 60px;
    height: 60px;
    border-radius: 50%;
    bottom: 15px;
    left: 15px;
    position: absolute;
  
}
.bott{
  width: 30%;
  background: orange;
}
.bott span{
  width: 30%;
  line-height: 60px;
 margin: 0 25px;
  font-size: 20px;
  
}
</style>