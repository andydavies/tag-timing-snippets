Adobe Target adds a style element with an id of `at-body-style` and the script below detects when this element is removed

See: https://experienceleague.adobe.com/docs/target/using/implement-target/client-side/at-js/manage-flicker-with-atjs.html?lang=en#managing-flicker-when-loading-at.js-asynchronously
 
``` js 
const callback = function(mutationsList, observer) {
   // Use traditional 'for loops' for IE 11
   for(const mutation of mutationsList) {
       for(const node of mutation.removedNodes) {
           if(node.nodeName === 'STYLE' && node.id === 'at-body-style') {
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
