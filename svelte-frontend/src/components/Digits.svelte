<script>
  export let time = '00'

  $: time = time.length > 1 ? time : `0${time}`
</script>

<span class="digits">{time}</span>

<style lang="scss">

  @import '../styles/colors';
    .digits {
      width: 123rem;
      height: 2.5rem;
    }
</style>
