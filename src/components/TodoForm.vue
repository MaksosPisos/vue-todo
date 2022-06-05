<script setup>
    defineProps(['newTodo'])
    defineEmits(['add-todo'])
</script>

<template>

      <form class="flex">
        <input
          type="text"
          class="input input-bordered w-full max-w-xs border-r-0 rounded-r-none"
          v-model="newTodo"
        />
        <button
          type="submit"
          class="btn border-l-0 rounded-l-none"
          @click.prevent="() => {
            $emit('add-todo', newTodo);
            newTodo = '';
          }"
          v-bind:disabled="newTodo.length < 3"
        >
          <i class="fa-duotone fa-magnifying-glass"></i>
        </button>
      </form>
      <div class="divider"></div>

</template>