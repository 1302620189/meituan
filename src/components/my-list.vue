<template>
    <div>
         <dl>
             <dt><img :src="pic" alt=""></dt>
             <dd>
                 <p>{{title}}</p>
                 <p>￥{{price}}</p>
                 <my-count :num="num" :id="id" :type="type"></my-count>
             </dd>
         </dl>
         
    </div>
</template>
<script>
import myCount from './my-count'// 购物车加加减减
export default {
    props:['title','price','id','num','type','pic'],
    components:{
        myCount
    },
    data(){
        return {

        }
    },
    computed:{

    },
    methods:{

    },
    created(){

    },
    mounted(){

    }
}
</script>
<style scoped lang="">
    dl{
        display: flex;
        margin: 10px;
        height: 120px;
    }
    dt{
        width:90px;
        height:90px;
        /* margin-top: 15px; */
        /* background: burlywood; */
    }
    dt img{
        width: 100%;
        height: 100%;
        margin-top: 15px;
    }
    dd{
        margin:0 7px;
    }
    dd p:nth-child(1){
        font-weight: 600;
        font-size: 19px;
    }
     dd p:nth-child(2){
        color: brown;
        font-size: 20px;
    }
    dd p{
        margin: 10px 0px;

    }
</style>