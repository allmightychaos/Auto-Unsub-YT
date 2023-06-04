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

<br>

## The Code

Either, via the [JavaScript File](./script.js) or copy the code here: 

```js
/**
 * YouTube bulk unsubscribe fn.
 * Wrapping this in an IIFE for browser compatibility.
 */

(async function iife() {
    // This is the time delay after which the "unsubscribe" button is "clicked"; 
    // Change it as per your need!
    var UNSUBSCRIBE_DELAY_TIME = 1000;

    /**
     * Delay runner. Wraps `setTimeout` so it can be `await`ed on.
     * @param {Function} fn
     * @param {number} delay
     */
    var runAfterDelay = (fn, delay) =>
        new Promise((resolve, reject) => {
        setTimeout(() => {
            fn();
            resolve();
        }, delay);
        });

    // Get the channel list; this can be considered a row in the page.
    var channels = Array.from(document.getElementsByTagName("ytd-channel-renderer"));
    if (!channels.length) {
        console.log("No channels found.");
        return;
    }
    else if (channels.length === 1) {
        console.log(`${channels.length} channel found.`);
    }
    else {
        console.log(`${channels.length} channels found.`);
    }
    
    var ctr = 0;
    for (const channel of channels) {
        // Get the subscribe button and trigger a "click"
        channel.querySelector(`[aria-label^='Unsubscribe from']`).click();

        await runAfterDelay(() => {
        // Get the dialog container...
        document.getElementsByTagName("yt-confirm-dialog-renderer")[0]
            // and find the confirm button...
            .querySelector(`[aria-label^='Unsubscribe']`)
            .click();

        console.log(`Unsubscribed ${ctr + 1}/${channels.length}`);
        ctr++;
        }, UNSUBSCRIBE_DELAY_TIME);
    }
})();
```

<br>

## Credits

Thanks to `Manessah de Graaf` for the idea + the original code, on [Adonis School](https://www.skool.com/adonis). <br>
If you want to join, you can use my [Affiliate Link](https://samuelweghofer--hamza.thrivecart.com/adonis-school-membership-copy-5/) to join! :) 