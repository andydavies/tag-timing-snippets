This snippet should be placed in the head of the document before the VWO async Smartcode.

VWO adds a style element with an id of `_vis_opt_path_hides`.

The snippet a MutationObserver to detect when the style element is added and then removed, generating a mark for each, and measure for the interval between them.

VWO also adds other temporary styles that hide other page elements too. 

See: https://help.vwo.com/hc/en-us/articles/900000743746-SmartCode-Checker-in-VWO

``` js
<script>
    callback = function(mutationsList, headObserver) {

        // Use traditional 'for loops' for IE 11
        for(mutation of mutationsList) {

            for(node of mutation.addedNodes) {
                if(node.nodeName === 'STYLE' && node.id === '_vis_opt_path_hides') {
                    performance.mark('vwo-hide-start');
                }

                if(node.nodeName === 'SCRIPT' && node.src.substr(0, "https://dev.visualwebsiteoptimizer.com/j.php".length) === "https://dev.visualwebsiteoptimizer.com/j.php") {
                    node.onload = function() {
                        performance.mark("vwo-loaded")
                    }
                }
            }
                            
            for(node of mutation.removedNodes) {
                if(node.nodeName === 'STYLE' && node.id === '_vis_opt_path_hides') {
                    performance.mark('vwo-hide-end');
                    performance.measure('vwo-hide-duration', 'vwo-hide-start', 'vwo-hide-end');
                }
            }
        }
    };

    headObserver = new MutationObserver(callback);

    headNode = document.getElementsByTagName('head')[0];
    headObserver.observe(headNode, { childList: true });
</script>```
