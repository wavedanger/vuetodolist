<template>
    <div>
        <h1 v-text="title"></h1>
       <div>
            <input type="text" v-model="newNames" @keyup.enter="onEnter">
        <button @click="onEnter">添加</button>
       </div>
        <ul  v-for="(item,index) in items">
        <li v-bind:id="index">
        <span v-bind:class="{check:item.check}" v-on:click="change(item)">{{item.name}}</span>    
         <span v-on:click="delName">删除</span>
        </li>
        
        </ul>
    </div>
</template>
<script>
import Store from '../../store.js'
export default {
    data(){
        return{
            check: false,
            title: 'this is a todolist',
           items:Store.fetch(),
           newNames:'wavedanger'
        }
    },
    watch:{
        items:{
            handler(items){
               Store.save(items)
            },
            deep:true
        }
    },
    methods:{
        change(item){
            item.check=!item.check;
          
        },
        onEnter(){
           if(this.newNames){
                this.items.push({name:this.newNames,check:false})
                console.log(this.newNames)
           }else{
               alert("不能为空！");
           }
        },
         delName(e){
            var id=e.target.parentNode.id
            this.items.splice(id,1)
        }
    }
}
</script>
<style>
    ul{
        list-style-type:none;
    }
    .check{
        text-decoration:underline;
    }
    input{width: 200px; height: 40px; font-size:20px;line-height:40px; margin:20px 0; outline:none; border:1px solid #333;}
     button{ width:60px; height: 40px; line-height:40px; background-color:#41b883; border: none; border-radius:5px; font-size:16px; color:#fff;}
</style>

