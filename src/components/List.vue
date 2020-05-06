<template>
  <div>
    <v-card
      :class="{'done': list.status === 'done'}"
      v-for="(list, index) in todoList"
      :key="index"
    >
      <p>{{ list.memo }}</p>
      <v-btn
        v-if="list.status === 'created'"
        @click="$emit('statusControl', index, 'done')"
        color="green"
      >
        <i>DONE</i><!--완료-->
      </v-btn>
      <v-btn
        v-else
        @click="$emit('statusControl', index, 'created')"
       color="blue"
      >
        <i>RECHECK</i><!--부활-->
      </v-btn>
      <v-btn 
        @click="$emit('listDelete', index)"
        color="red"
      >
        <i>DELETE</i>
      </v-btn>
      <v-btn
        @click="listEdit(list.memo, index)"
        v-if="list.status === 'created'"
        color="yellow"
      >
        <i>EDIT</i>
      </v-btn>
    </v-card>
  </div>
</template>

<script>
import { eventBus } from "../main"
export default {
  props: ["todoList"],
  methods: {
    listEdit(memo, index) {
      eventBus.listEdit(memo, index)
    }
  }
}
</script>

<style scoped>
.done {
  background-color: rgba(0, 0, 0, 0.1);
}
.done p {
  text-decoration: line-through;
  color: rgba(0, 0, 0, 0.5);
}
b-btn{
  border:1px solid #333;
}
</style>