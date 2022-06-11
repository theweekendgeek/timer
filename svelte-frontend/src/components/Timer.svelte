<script>
    // import store and use values from there
    import Digits from "./Digits.svelte";
    import Button from "./Button.svelte";

    import {derived, writable} from "svelte/store";

    let intervalRef

    export const seconds = writable(120)

    export const minutesLeft = derived(
        seconds,
        $seconds => Math.floor($seconds / 60),
        2
    )

    export const secondsLeft = derived(
        [seconds, minutesLeft],
        ([$seconds, $minutesLeft]) => $seconds - ($minutesLeft * 60),
        0
    )

    function checkStop(seconds) {
        if (seconds > 0) return


        stopTimer()
        console.log('DONEDONEDONE')

    }

    $: checkStop($seconds)

    function startTimer() {
        intervalRef = setInterval(() => {
            $seconds = $seconds - 1
        }, 1000)
    }

    function stopTimer() {
        if (!intervalRef) return

        clearInterval(intervalRef)
    }

    function reset() {
        $seconds = 120
    }
</script>

<div id="timer">
    <div id="container">
        <div id="time">
            <div id="clock">
                <Digits time={`${$minutesLeft}`}/>
                :
                <Digits time={`${$secondsLeft}`}/>
            </div></div>
        <div id="controls">
            <Button title="Start" clickHandler={startTimer}/>
            <Button title="Stop" clickHandler={stopTimer}/>
            <Button title="Reset" clickHandler={reset}/>
        </div>
    </div>
</div>

<style lang="scss">
  @import '../styles/colors';
  #container {
    height: 95vh;
    width: 95vh;
    margin: auto;
    display: grid;
    grid-template-rows: 30% auto 30%;

    grid-template-columns: 20% auto 20%;
  }

  #time {
    grid-column: 2 / 3;
    grid-row: 2 / 3;
    display: flex;
  }

  #clock {
    margin: auto;
    font-size: $timer-font-size;
  }

  #controls {
    grid-column: 2 / 3;
    grid-row: 3 / 4;
    display: flex;
    justify-content: space-between;

  }
</style>
