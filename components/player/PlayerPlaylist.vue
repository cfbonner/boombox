<template>
  <ul class="flex flex-col text-xs h-full overflow-y-scroll list-disc border-b border-black divide-y divide-black">
    <li v-for="(song, i) in songs" class="flex w-full h-full">
      <button v-on:click.prevent="selectSong(i)"
              href="#"
              class="flex items-center w-full px-4 py-4 hover:bg-yellow-500"
              v-bind:class="{'bg-yellow-500':index == i && playing}">
         <img class="w-4 h-full mr-4" src="~/assets/images/play.svg" v-if="(index == i && !playing) || (index != i)" />
         <img class="w-4 h-full mr-4" src="~/assets/images/pause.svg" v-if="index == i && playing" />
         <span class="h-full">{{ song.title }}</span>
      </button>
    </li>
  </ul>
</template>

<script>
export default {
  props: {
    songs: Array,
    index: Number,
    playing: Boolean,
  },
  methods: {
    selectSong(new_index) {
      this.$emit('update:index', new_index)
      if (!this.playing) {
        this.$emit('update:playing', true)
      }
    }
  }
}
</script>

<style>
img.hidden {
  @apply invisible
}
/style>
