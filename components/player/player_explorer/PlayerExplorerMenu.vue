<template>
  <nav>
    <ul class="menu divide-x  divide-black">
      <li class="menu-item" v-if="playlist_selected">
        <a v-on:click.prevent="viewAll">
          <img class="w-full h-full" src="~/assets/images/grid.svg" />
        </a>
      </li>
      <!-- <li class="menu-item"> -->
      <!--   <a v-on:click.prevent="viewAll"> -->
      <!--     <img class="w-full h-full" src="~/assets/images/list.svg" v-if="" /> -->
      <!--   </a> -->
      <!-- </li> -->
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

<style>
.menu {
  @apply h-12 flex justify-end items-center border-b border-black;
}

.menu-item:first-child {
  @apply border-l border-black;
}
.menu-item {
  @apply flex items-center p-3;
}

</style>
