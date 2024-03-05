<template>
<v-container>
    <v-layout row wrap>
      <v-flex xs12 text-xs-center>
        <h1 class="pb-2">To Do List</h1>
        <p>All: {{ todoList.length }} / Completed: {{ countDone}} / Left: {{ todoList.length - countDone }}</p>
      </v-flex>
      <v-flex xs6 pa-2>
        <list 
          :todoList="todoList" 
          @statusControl="statusControl" 
          @listDelete="listDelete" />
      </v-flex>
      <v-flex xs6 pa-2>
        <list-add 
          @listAdd="listAdd" 
          @listEdit="listEdit" />
      </v-flex>
    </v-layout>
</v-container>
</template>

<script>
import List from './List.vue'
import ListAdd from './ListAdd.vue'
export default {
  components: { 
    List, 
    ListAdd 
  },
  data() {
    return {
      todoList: [],
    }
  },
  computed: {
    countDone() {
      let count = 0;
      this.todoList.forEach(list => {
        if(list.status === 'done') count++;
      });
      return count;
    }
  },
  methods: {
    listAdd(memo) {
      this.todoList.push({ memo, status: 'created' });
    },
    statusControl(index, status) {
      this.todoList[index].status = status;
    },
    listDelete(index) {
      this.todoList.splice(index, 1);
    },
    listEdit(memo, index) {
      this.todoList[index].memo = memo;
    },
  }
}
</script>