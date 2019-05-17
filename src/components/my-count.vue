<template>
    <div>
        
            <span @click="del">-</span>
            <span>{{num}}</span>
            <span @click="add">+</span>
      
        
    </div>
</template>


<script>

export default {
    props:["num","id","type"],
    components:{

    },
    data(){
        return {};
    },
    computed:{

    },
    methods:{
        add(){
            let num =this.num + 1;
            this.$bus.$emit('addCount',num.this.id)
        },
        del(){
            let num =this.num - 1;
            this.$bus.$emit("addCount",num.this.id);
        }
    },
    created(){

    },
    mounted(){

    }
}
</script>
<style scoped lang="">
div{
    margin-left:45px;
    font-size: 18px;
}
div div span:nth-child(1){
    width: 25px;
    height: 25px;
    line-height: 25px;
    border: 1px solid #ccc;
    border-radius: 50%;
    display: inline-block;
    text-align: center;
  
}
span:nth-child(3){
    width: 25px;
    height: 25px;
    line-height: 25px;
    border: 1px solid #ccc;
    border-radius: 50%;
    display: inline-block;
    text-align: center;
    background: orange;
}
</style>