<template>
    <div>
        <form @submit="addTodo">
        <input type='text' v-model="title" name='title' >
        <button type="submit">Submit</button>
       </form> </div>
</template>
<script>
export default {
    name:"AddTodo",
    methods:{
addTodo(){
    event.preventDefault();
    const newTodo={
            title:this.title,
        completed:false
    }
    //send upto  parent
    this.$emit("add-todo",newTodo);
   this.title='';
    }
    },
    data(){
        return{
            title:''
        }
    }
}
</script>
<style scoped>
 form {
    display: flex;
  }
  input[type="text"] {
    flex: 10;
    padding: 5px;
  }
  input[type="submit"] {
    flex: 2;
    color: green;

  }

</style>