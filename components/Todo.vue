<template>
  <li class="relative flex justify-between mb-4">
    <label class="inline-flex items-center">
      <input
        type="checkbox"
        class="form-checkbox"
        :checked="state"
        @change="toggleCheck" />
      <span class="ml-2">{{title}}</span>
    </label>
    <button @click="deleteTodo">
      x
    </button>
  </li>
</template>
<script>
export default {
  props: {
    state:{
      type: Boolean,
      default: false
    },
    title:{
      type: String,
      required: true
    },
  },
  methods:{
    toggleCheck(){
      this.$emit('state:changed', !this.state);
    },
    deleteTodo(){
      this.$emit('todo:delete');
    }
  }
}
</script>
