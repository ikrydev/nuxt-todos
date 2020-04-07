<template>
  <div class="flex py-4 border-t border-gray-900 justify-between">
    <div class="flex">
      <button :class="filter === 'all' && 'active'" @click="setFilter('all')">
        All
      </button>
      <button :class="filter === 'completed' && 'active'" @click="setFilter('completed')">
        Completed
      </button>
    </div>
    <div class="flex">
      <button class="text-red-500" @click="clear">
        Clear Completed
      </button>
    </div>
  </div>
</template>
<script>
export default {
  props:{
    filter:{
      type: String,
      default: 'all'
    }
  },
  methods:{
    setFilter(value){
      this.$emit('filter:set', value);
    },
    clear(){
      this.$emit('clear');
    }
  }
}
</script>
<style lang="postcss" scoped>
button{
  @apply text-xs mr-3;
}
button:focus{
  @apply outline-none;
}
buttonL:hover{
  @apply underline;
}
.active{
  @apply font-bold text-green-500;
}
</style>
