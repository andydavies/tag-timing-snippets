# Google Publisher Tag (gpt.js)

Until August 2022, GPT added three marks of it's own but these seem to have been removed
- `gpt-tag-load`
- `gpt-first-ad-request`
- `gpt-first-ad-render`


GPT also fires events related to each individual add unit e.g. when it's visiblity changes, when an ad is requested for a slot etc., see https://developers.google.com/publisher-tag/reference#googletag.events.event for more details.

By listenting to these events we can create User Timing marks to record when they occur.


```js
var googletag = googletag || {};
googletag.cmd = googletag.cmd || [];

googletag.cmd.push(function() {
    // This listener will be called when an impression loads.
    googletag.pubads().addEventListener('slotOnload', function(event) {
        performance.mark('adslot-' + event.slot.getSlotElementId() + '-loaded');
    });
});
```