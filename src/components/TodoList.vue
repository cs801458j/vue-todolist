<template>
  <div>
  <ul>
    <li v-for="(todoItem, index) in todoItems" v-bind:key="todoItem.item" class="shadow">
      <i class="checkBtn fas fa-check"  v-bind:class="{checkBtnCompleted: todoItem.completed}" 
      v-on:click="toggleComplete(todoItem, index)"></i>
      <span v-bind:class="{textCompleted: todoItem.completed}">{{ todoItem.item }}</span>
      <span class="removeBtn" v-on:click="removeTodo(todoItem, index)" >
      <i class="fas fa-trash-alt"></i>
      </span>
    </li>
  </ul>
  </div> 
</template>

<script>
export default {
  data: function() {
    return {
      todoItems: []
    }
  },
  methods: {
    removeTodo: function(todoItem, index) {
      console.log(todoItem, index);
      localStorage.removeItem(todoItem);
      this.todoItems.splice(index,1); //  기존 배열을 변경해서 새로운 배열
    },
    toggleComplete: function(todoItem, index) {
      todoItem.completed = !todoItem.completed;
      localStorage.removeItem(todoItem.item);
      //  로컬스토리지 데이터 갱신하는 부분
      localStorage.setItem(todoItem.item, JSON.stringify(todoItem));
      console.log(todoItem, index);
    }
  },
  //  생성 시점에 이 안에 로직이 한번 호출됨
  created: function() {
    if(localStorage.length > 0){
      for(var i =0; i < localStorage.length; i++){
        if(localStorage.key(i) !== 'loglevel:webpack-dev-server'){
          this.todoItems.push(JSON.parse(localStorage.getItem(localStorage.key(i))));
          
          //this.todoItems.push(localStorage.key(i));
        }
          
      }
    }
  }
}
</script>

<style>
  ul {
    list-style-type: none;
    padding-left: 0px;
    margin-top: 0;
    text-align: left;
  }
  li {
    display: flex;
    min-height: 50px;
    height: 50px;
    line-height: 50px;
    margin: 0.5rem 0;
    padding: 0 0.9rem;
    background: white;
    border-radius: 5px;
  }

  .removeBtn {
    margin-left: auto;
    color: #de4343;
  }
  .checkBtn {
    line-height: 50px;
    color: #62acde;
    margin: auto 0;
    margin-right: 10px;
       
  } 
  .checkBtnCompleted {
    color : #b3adad;
  } 
  .textCompleted {
    text-decoration: line-through;
    color: #b3adad;
  }

</style>