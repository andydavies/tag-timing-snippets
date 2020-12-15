Google Optimize adds an `async-hide` class to the html element so the script detects when this class is removed.

See: https://developers.google.com/optimize#the_anti-flicker_snippet_code


``` js
const callback = function(mutationsList, observer) {
   // Use traditional 'for loops' for IE 11
   for(const mutation of mutationsList) {
       if(!mutation.target.classList.contains('async-hide') && mutation.attributeName === 'class' && mutation.oldValue.includes('async-hide')) {
           performance.mark('anti-flicker-end');
          
           observer.disconnect();
 
           break;
       }
   }
};
 
const observer = new MutationObserver(callback);
 
const node = document.getElementsByTagName('html')[0];
observer.observe(node, { attributes: true, attributeOldValue: true });

```
