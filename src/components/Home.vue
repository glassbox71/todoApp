<template>
<v-container>

    <v-flex>
      <h1>투두 리스트</h1>
      <p>전체 할일: {{ todoList.length }} / 완료된 할일: {{ countDone }} / 남은 할일: {{ todoList.length -  countDone}}</p>
    </v-flex>
    
    <v-flex>
      <ListAdd
        @listAdd="listAdd"
        @listEdit="listEdit"
      />
    </v-flex> 
    <v-flex>
      <List
        :todoList="todoList"
        @statusControl="statusControl"
        @listDelete="listDelete"
      />
    </v-flex> 
</v-container>
</template>

<script>
import List from "./List"
import ListAdd from "./ListAdd"

export default {
  components: {
    List,
    ListAdd
  },
  data() {
    return {
      todoList: []
    }
  },
  created() {
    console.log(this)
  },
  computed: {
    countDone() {
      let count = 0
      this.todoList.forEach(list => {
        if (list.status === "done") count++
      })
      return count
    }
  },
  methods: {
    listAdd(memo) {
      console.log("받았어!")
      this.todoList.push({ memo: memo, status: "created" })
    },
    statusControl(index, status) {
      this.todoList[index].status = status
    },
    listDelete(index) {
      this.todoList.splice(index, 1)
    },
    listEdit(memo, index) {
      this.todoList[index].memo = memo
    }
  }
}
</script>