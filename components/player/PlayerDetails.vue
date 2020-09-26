<template>
  <div class="boombox-section space-y-1">
    <div class="align-middle text-xs font-bold"><span>{{ prettyCurrentTime || '00:00' }}</span> / <span>{{ prettyCurrentDuration || '00:00' }}</span></div>
    <div class="text-sm"><span>{{ current_title }}</span> - <span>{{ current_artist }}</span></div>
  </div>
</template>

<script>

</script>

<script>
const paddedNumber = number => {
  if (Number.isNaN(number)) { return '00' }

  if (number >= 10) {
    return `${number}`
  } else {
    return `0${number}`
  }
}

const prettyTime = (seconds) => {
  if (Number.isNaN(seconds)) { return }

  if (seconds < 60) {
    const remainingSeconds = Math.ceil(seconds)
    return `00:${paddedNumber(remainingSeconds)}`
  } else {
    const minutes = Math.ceil(seconds / 60)
    const remainingSeconds = seconds % minutes
    return `${paddedNumber(minutes)}:${paddedNumber(Math.ceil(remainingSeconds))}`
  }
}

module.exports = {
  props: {
    current_time: Number,
    current_duration: Number,
    current_title: String,
    current_artist: String
  },
  computed: {
    prettyCurrentTime: function() {
      return prettyTime(this.current_time)
    },
    prettyCurrentDuration: function() {
      return prettyTime(this.current_duration)
    },
  },
}
</script>
