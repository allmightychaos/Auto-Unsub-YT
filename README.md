# Auto-Unsub-YT

## How to use:

Copy the code from the [JavaScript File](./script.js) and paste it into the console of your browser's developer tools while on the [YouTube subscriptions page](https://www.youtube.com/feed/channels).
<br>
To open the developer tools, press `Ctrl+Shift+I` on Windows or `Cmd+Opt+I` on Mac, then select the "Console" tab.

<br>

## Code Breakdown:

* Using IIFE (immediately-invoked function expression) for borwser compaitbility
* `UNSUBSCRIBE_DELAY_TIME` variable after when the unsubscribe button should be clicked (in ms)
* `runAfterDelay` function is defined to wrap the `setTimeout` function and allow awaiting its execution
* `channels` variable are all channels found on the page
* Number of channels found → logged to the console.
* `ctr` is created to track the progress of unsubscribing.
* A `for...of` loop iterates over each channel