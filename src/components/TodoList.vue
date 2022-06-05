<script setup>
    defineProps(["itemComplete", "itemTitle"]);
    defineEmits(["modal-window"])
</script>

<template>
  <li
    class="bg-base-300 p-2 rounded-md shadow-md transition-all"
    v-bind:class="{
      'opacity-60': itemComplete,
      'line-through': itemComplete,
    }"
  >
    <div class="flex items-center justify-between">
      <h3 class="" v-bind:class="{ italic: itemComplete }">
        {{ itemTitle }}
      </h3>
      <div class="flex gap-4">
        <button
          class="bg-green-400 text-slate-800 py-2 px-3 rounded-xl"
          @click="() => (itemComplete = !itemComplete)"
        >
          <i class="fa-duotone fa-circle-check"></i>
        </button>
        <button
          class="bg-rose-400 text-slate-800 py-2 px-3 rounded-xl"
          @click="$emit('modal-window', index)"
        >
          <i class="fa-duotone fa-ban"></i>
        </button>
      </div>
    </div>
  </li>
</template>
