<template>
  <div>
  <ul>
    <li v-for="todoItem in todoItems" v-bind:key="todoItem">
      {{ todoItem}}
    </li>
    <!-- <li>hello</li>
    <li>hi</li>
    <li>bye</li>
    <li>hello</li> -->
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
  //  생성 시점에 이 안에 로직이 한번 호출됨
  created: function() {
    if(localStorage.length > 0){
      for(var i =0; i < localStorage.length; i++){
        if(localStorage.key(i) !== 'loglevel:webpack-dev-server'){
          this.todoItems.push(localStorage.key(i));
        }
          
      }
    }

    console.log('created');
  }
}
</script>

<style>

</style>