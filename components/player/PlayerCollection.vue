<template>
  <ul class="flex flex-col text-xs h-full overflow-y-scroll list-disc border-b border-black divide-y divide-black">
    <li v-for="(playlist, i) in collection" class="flex w-full h-auto">
      <button v-on:click.prevent="selectPlaylist(i)"
              class="flex items-center w-full px-4 py-4 hover:bg-yellow-500"
              >
         <img class="w-4 h-full mr-4" src="~/assets/images/play.svg" />
         <span class="h-full">{{ playlist.title }}</span>
      </button>
    </li>
  </ul>
</template>

<script>
export default {
  props: {
    collection: Array,
    collection_index: Number,
    collection_selected: Boolean,
  },
  methods: {
    selectPlaylist(index) {
      this.$emit('selectPlaylist', index)
    }
  }
}
</script>

<style>
img.hidden {
  @apply invisible
}
/style>
