Google Optimize adds an `async-hide` class to the html element so the script detects when this class is removed.

See: https://developers.google.com/optimize#the_anti-flicker_snippet_code

Place this code directly after the anti-flicker snippet

``` js
(function (node, selector, name) {

    performance.mark(name + '-start');

    const callback = function (mutationsList, observer) {

        // Use traditional 'for loops' for IE 11 support
        for (const mutation of mutationsList) {

            if (mutation.attributeName === 'class' &&
                !mutation.target.classList.contains(selector) &&
                mutation.oldValue.includes(selector)) {

                    performance.mark(name + '-end');
                    performance.measure(name + '-duration', name + '-start', name + '-end');

                    observer.disconnect();
                    break;
            }
        }
    }

    const observer = new MutationObserver(callback);
    observer.observe(node, { attributes: true, attributeOldValue: true });

})(document.documentElement, 'async-hide', 'anti-flicker');
```
