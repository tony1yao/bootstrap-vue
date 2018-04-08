<template>
  <div id="todo">  
      <h1>This is a simple todo list</h1>
      <input type="text" placeholder="please input your todo task" @keyup.enter="addItem">
      <div id="content">
          <div id="header">
              <input type="button" value="All" @click="setStatus('All')">
              <input type="button" value="New" @click="setStatus('New')">
              <input type="button" value="Completed" @click="setStatus('Completed')">
          </div>
          <div id="body">
          <ul v-for="item in getShowItems" :key=item.text>
              <li>
                    <div>
                        <input type="checkbox" name="completed" id="checkbox" v-model="item.completed">
                        <label :class="[item.completed?'completed':'']">{{item.text}}</label>
                        <input type="button" value="delete" @click="deleteItem(item)">
                    </div>
                </li>
          </ul>
          </div>
      </div>
  </div>
</template>


<script>
export default {
  data(){
      return{
          items:[],
          status: 'All'
      }
  },
  computed:{
      getShowItems(){
          if(this.status === 'All'){
              return this.items;
          }
          const completed = this.status === 'Completed'
          return this.items.filter(item => item.completed === completed)
      }
  },
  methods:{
      addItem(e){
          console.log("key pressed")
          this.items.unshift({
              completed:false,
              text: e.target.value.trim()
          })
          e.target.value = ''
      },

      toggle(item){
          item.completed = !item.completed
      },

      deleteItem(item){
          console.log("inside of delete item")
          this.items.splice(this.items.findIndex(i => i ===item),1)
      },

      setStatus(status){
          console.log("inside of setStatus, and the status is "+status)
          this.status = status
      }
  }
}
</script>

<style lang="stylus" scoped>
.completed{
    color #d9d9d9
    text-decoration line-through
}
</style>
