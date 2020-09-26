<template>
  <nav>
    <ul>
      <li>
        <a v-on:click.prevent="viewAll">
          <span class="sr-only">Albums</span>
          <img class="w-8 h-8 mr-4" src="~/assets/images/grid.svg" v-if="!playlist_selected" />
          <img class="w-8 h-8 mr-4" src="~/assets/images/list.svg" v-if="playlist_selected" />
        </a>
      </li>
    </ul>
  </nav>
</template>

<script>
export default {
  props: {
    playlist_selected: Boolean
  },
  methods: {
    viewAll() {
      this.$emit('viewAll')
    }
  }
}
</script>
