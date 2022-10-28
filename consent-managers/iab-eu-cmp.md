# IAB EU Consent Management Platforms (CMPs)

Often from from *.mgr.consensu.org

IAB EU CMPs Exposes an API (__tcfapi) that adtech vendors can hook into. 

We can also listen to events from this API to understand the state of the CMP e.g. when's the UI shown, when does the user dismiss it, and if the user has already given content (or not) when is the CMP ready to respond to adtech

- `cmpuishown` (consent UI is shown to user)
- `useractioncomplete` (user dismissed UI and CMP is ready to respond to adtech)
- `tcloaded` (Constent has previously given or no, and CMP is ready to respond to adtech)

Assuming the user doesn't relaunch the consent dialog later each page should have either `cmpuishown` and `useractioncomplete` marks or a `tcloaded` mark

From a performance monitoring perspective `cmpuishown` and `tcloaded` seem to the the two most interesting to track. The first measures how quickly the consent dialog is displayed, the second when the CMP is ready to respond to adtech (when the dialog isn't shown)

This sample creates User Timing marks for each of the three events once.

It should be placed directly after the CMP stub in the page

**Note** the marks may not line up with a filmstrip from a synthetic test, or devtools, for example many CMPs fire the `cmpuishown` event before the consent dialog is visible on the screen

```
// Creates User Timing marks for cmpuishown, useractioncomplete & tcloaded
if (typeof window.__tcfapi === 'function') {
    
    let markedEvents = [];
    window.__tcfapi('addEventListener', 2, (tcdata, success) => { 

        if(success && !markedEvents.includes(tcdata.eventStatus)) { 

            performance.mark('tcf-' + tcdata.eventStatus); 

            // Prevent listening to events twice, to prevent generation of extra 
            // cpuishown & useractioncomplete marks if visitor reopens CMP UI
            markedEvents.push(tcdata.eventStatus);
        }
    });
}
```
