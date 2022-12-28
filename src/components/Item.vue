<template>
  <div id="item">
    <ul>
        <li v-for="task in lista" :key="task.key">
            <span>{{ task.text }}</span>
            <button @click="delItem(task.key)">Concluir</button>
        </li>
    </ul>
  </div>
</template>

<script>
export default {
    name: 'Item',
    props:[
        'lista',
        'delete'
    ],
    methods:{
        delItem(key){
            this.delete(key);
        }
    }

}
</script>

<style scoped>
    #item{
        white-space: pre-line;
        word-wrap: break-word;
    }

    ul{
        list-style: none;
        padding: 15px;
        margin-top: 20px;
    }

    li:not(:first-child){
        border-top: 1px  solid #eee;
    }

    ul li{
        padding: 15px 0;
        display: flex;
        flex-direction: row;
        align-items: center;
        justify-content: space-between;
    }

    span{
        color: #0d2636;
    }

    button{
        cursor: pointer;
        background: #DDD;
        color: #000;
        border: 0;
        border-radius: 4px;
        padding: 8px 9px;
        outline: none;
    }
</style>