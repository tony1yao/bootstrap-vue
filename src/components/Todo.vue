<template>
  <div id="todo" class="container">  
      <h1>This is a simple todo list</h1>
      <input type="text" class="form-control" placeholder="please input your todo item and press Enter." @keyup.enter="addItem">
            <ul class="nav nav-pills">
              <li class="nav-item">
                  <a class="nav-link" :class="this.status==='All'?'active':''"  @click="setStatus('All')">All</a>
              </li>
              <li class="nav-item">
                  <a class="nav-link" :class="this.status==='New'?'active':''" @click="setStatus('New')">New</a>
              </li>
              <li class="nav-item">
                  <a class="nav-link" :class="this.status==='Completed'?'active':''" @click="setStatus('Completed')">Completed</a>
              </li>
          </ul>
    <table class="table .table-striped table-sm table-hover">
        <thead>
            <tr>
                <th>Mark as done</th>
                <th>Item content</th>
                <th>Delete the item</th>
            </tr>
        </thead>
        <tbody>
            <tr v-for="item in getShowItems" :key=item.text>
                <td><input type="checkbox" name="completed" id="checkbox" v-model="item.completed"></td>
                <td><p :class="[item.completed?'completed':'']" class=".font-weight-normal">{{item.text}}</p></td>
                <td><button class="btn btn-link" @click="deleteItem(item)">Delete</button></td>
            </tr>
        </tbody>
    </table>
  </div>
</template>


<script>
export default {
  data() {
    return {
      items: [],
      status: "All"
    };
  },
  computed: {
    getShowItems() {
      if (this.status === "All") {
        return this.items;
      }
      const completed = this.status === "Completed";
      return this.items.filter(item => item.completed === completed);
    }
  },
  methods: {
    addItem(e) {
      console.log("key pressed");
      this.items.unshift({
        completed: false,
        text: e.target.value.trim()
      });
      e.target.value = "";
    },

    toggle(item) {
      item.completed = !item.completed;
    },

    deleteItem(item) {
      console.log("inside of delete item");
      this.items.splice(this.items.findIndex(i => i === item), 1);
    },

    setStatus(status) {
      console.log("inside of setStatus, and the status is " + status);
      this.status = status;
    }
  }
};
</script>

<style lang="stylus" scoped>
.completed {
    color: #d9d9d9;
    text-decoration: line-through;
}

table tbody tr td input p button{
            vertical-align: middle;
        }
</style>
