VWO adds a style element with an id of `_vis_opt_path_hides` and as with Adobe Target the script detects then this is removed.

VWO also adds other temporary styles that hide other page elements too. 

See: https://help.vwo.com/hc/en-us/articles/900000743746-SmartCode-Checker-in-VWO

``` js
const callback = function(mutationsList, observer) {
   // Use traditional 'for loops' for IE 11
   for(const mutation of mutationsList) {
       for(const node of mutation.removedNodes) {
           if(node.nodeName === 'STYLE' && node.id === '_vis_opt_path_hides') {
               performance.mark('anti-flicker-end');
 
               observer.disconnect();
 
               break;
           }
       }
   }
};
 
const observer = new MutationObserver(callback);
 
const node = document.getElementsByTagName('head')[0];
observer.observe(node, { childList: true });
```
