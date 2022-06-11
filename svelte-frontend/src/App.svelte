<script>
    import logo from './assets/svelte.png'
    import Counter from './lib/Counter.svelte'
    import {onMount} from "svelte";
    import Timer from "./components/Timer.svelte";

    onMount(async () => {
        console.log(1)

        Neutralino.init()
        // await Neutralino.events.on('ready', () => {
        //     // console.log('ready');
        // });


        await Neutralino.events.on('windowClose', () => {
            Neutralino.app.exit()
        });

        console.log(3)
    })
</script>

<main>
    <Timer/>
</main>

<style lang="scss">
  @import "./styles/colors";
  //@use './styles/colors' as *;

  :root {
    font-family: Cantarell, -apple-system, BlinkMacSystemFont, 'Segoe UI', Roboto, Oxygen,
    Ubuntu, 'Open Sans', 'Helvetica Neue', sans-serif;
  }

  :global(body) {
    background: $background;
    color: $font-color;
  }


</style>
