<template>
  <div>
    <h1>Todo Apps</h1>
      <div class="w-full">
        <input
          class="field-input"
          type="text"
          placeholder="Write Some Todo"
          @keypress.enter="addTodo"
          v-model="title">
      </div>
      <ul class="list">
        <todo-list
          v-for="(todo, index) in filteredTodos()"
          :key="index"
          :title="todo.title"
          :state="todo.state"
          @state:changed="(state) => stateChanged(index, state)"
          @todo:delete="deleteTodo(todo.id)"
          >
        </todo-list>
      </ul>
      <filter-section
        :filter="filter"
        @filter:set="setFilter"
        @clear="clear">
      </filter-section>
  </div>
</template>

<script>
import TodoList from '~/components/Todo.vue'
import FilterSection from '~/components/Filter.vue'

export default {
  components: {
    TodoList,
    FilterSection
  },
  data: function(){
    return{
      todos: [],
      title:'',
      filter: 'all'
    }
  },
  methods:{
    filteredTodos(){
      return this.filter === 'completed' ? this.todos.filter(todo => todo.state === true) : this.todos;
    },
    addTodo(){
      const id = new Date().getMilliseconds() * 99;
      this.todos = [
        ...this.todos,
        {
          id,
          title: this.title,
          state: false
        }
      ];
      this.title = '';
    },
    stateChanged(selectedIndex,newState){
      this.todos = this.todos.map((todo,index) => {
        return index === selectedIndex ? {
          ...todo,
          state: newState
        } : todo;
      });
    },
    deleteTodo(selectedID) {
      this.todos = this.todos.filter(todo => todo.id !== selectedID);
    },
    setFilter(value){
      this.filter = value;
    },
    clear(){
      this.todos = this.todos.map(todo => ({
        ...todo,
        state : false
      }))
    }
  }
}
</script>

<style lang="postcss" scoped>
h1{
  @apply text-2xl block font-bold py-6 text-gray-400 tracking-widest text-center;
}
.list{
  @apply m-0 my-4 p-0 list-none w-full;
}
.field-input {
  @apply bg-gray-200 appearance-none border-2 border-gray-200 rounded w-full py-2 px-4 text-gray-700 leading-tight;
}
.field-input:focus{
  @apply outline-none bg-white border-purple-500;
}
</style>

