<template>
  <div>
    <header>
      <h1 class="sr-only">
        boombox
      </h1>
    </header>
    <main>
      <Player v-bind:songs="songs"/>
    </main>
  </div>
</template>

<script>
export default {
  data: () => {
    return {
      songs: [
        {
          src: '/audio/zante/1.webm',
          title: 'Can I Eat',
          author: 'Cutty\'s Gym'
        },
        {
          src: '/audio/zante/2.webm',
          title: 'Dance Stance',
          author: 'Cutty\'s Gym'
        },
        {
          src: '/audio/zante/3.webm',
          title: 'Batboy',
          author: 'Cutty\'s Gym'
        },
      ]
    }
  }
}
</script>

<style>
.container {
  margin: 0 auto;
  min-height: 100vh;
  display: flex;
  justify-content: center;
  align-items: center;
  text-align: center;
}

.title {
  font-family:
    'Quicksand',
    'Source Sans Pro',
    -apple-system,
    BlinkMacSystemFont,
    'Segoe UI',
    Roboto,
    'Helvetica Neue',
    Arial,
    sans-serif;
  display: block;
  font-weight: 300;
  font-size: 100px;
  color: #35495e;
  letter-spacing: 1px;
}
</style>
