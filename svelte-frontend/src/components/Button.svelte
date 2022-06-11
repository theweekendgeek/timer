<script>
  export let title = ""
  export let clickHandler = null
</script>

<button on:click={clickHandler ?? clickHandler}>{title}</button>

<style lang="scss">
    @import '../styles/colors';

    $button_radius: 6px;

    button {
      background: $buttonBackground;
      color: $font-color;
      height: 3rem;
      width: 5rem;
      padding: 5px 10px;
      border-radius: $button_radius;
      font-weight: bold;
      border: 1px solid $button-border;
      &:hover {
        background: lighten($buttonBackground, 2%);
      }

      &:active {
        background: #000000;
      }

    }
</style>
