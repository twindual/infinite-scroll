# Infinite Scroll

<http://www.infinite-scroll.com/>

The jQuery and WordPress Plugins:

* jQuery Plugin `v2.2.0`
* WordPress Plugin <http://www.infinite-scroll.com/installation/>

Requires jQuery v1.7 or more recent.

Tested with jQuery v1.12.4, v2.2.4 and v3.1.1 from the Google CDN.

##Methods##
A method is a command you can use to control Infinite Scroll once the plugin has been initialized. You can call on any Infinite Scroll method by using `$('.selector').infinitescroll('method-name');`.

**Bind**  
`$('.selector').infinitescroll('bind');`  
Binds selector to check on scroll to see if the plugin needs to load more content.

**Unbind**  
`$('.selector').infinitescroll('unbind');`  
Unbinds selector to check on scroll to see if the plugin needs to load more content.

**Destroy**  
`$('.selector').infinitescroll('destroy');`  
Destroys the instance of infinite scroll. This is create a flag to not load anymore content and will unbind all events.

**Pause**  
`$('.selector').infinitescroll('pause');`  
Pausing the plugin will temporarily create a flag to not retrieve content on scroll. To unpause, use the method `resume`.

**Resume**  
`$('.selector').infinitescroll('resume');`  
Resumes the instance of infinite scroll. This is create a flag to load more content and will bind events.

**Toggle**  
`$('.selector').infinitescroll('toggle');`  
Toggling will switch the `pause` value of the plugin, either pausing or resuming the plugin.

**Retrieve**  
`$('.selector').infinitescroll('retrieve');`  
Retrieve will load the next page of content if available.

**Scroll**  
`$('.selector').infinitescroll('scroll');`  
Scroll will check to see if the next page is to be loaded, the same thing as if a user scrolled.

**Update**  
`$('.selector').infinitescroll('update', {debug: true});`  
The `update` method is used to update options in the instance of Infinite Scroll after initialization. The second argument is the object of options that you want to update.


##Options##
Better documentation coming soon.

```javascript
$('.selector').infinitescroll({
        debug: false,               // Toggle diplays of debugging messages via console.log().
        infid: 0,                   //Instance ID

        // Page result loading params.
        loading: {
            // Function hooks.
            start: undefined,       // Triggers BEFORE first fetch of the next page results.
            finished: undefined,    // Triggers AFTER appending the data to existing results list.

            // Message display params.
            selector: null,         // Puts the load message in a specific selector. Defaults to the contentSelector.
            msgText: '<em>Loading the next set of posts...</em>',
            finishedMsg: "<em>Congratulations, you've reached the end of the internet.</em>",
            msg: null,              // Contains the HTML of the loading message. Gets generated from the option values.
            speed: 'fast',          // When 'animate' is TRUE it sets the speed of the jQuery animate function.
            img: 'img/loading-spinner.gif',
        },
        state: {
            isDuringAjax: false,
            isInvalidPage: false,
            isDestroyed: false,
            isDone: false,          // TRUE when no more results pages to fetch.
            isPaused: false,
            isBeyondMaxPage: false,
            currPage: 1
        },

        errorCallback: function () { }, // Callback function
        behavior: undefined,        // Used to over-ride a single default function behaviour.
                                    // Requires a function added to the initialization options that begins with the same function name you want to 
                                    // over-ride followed by the underscore '_', and followed by whatever unique string value you set in 'behaviour'.

        // jQuery selectors.
        navSelector: 'a [title="Next"]',
        nextSelector: 'div.navigation a:first',
        itemSelector: 'div [data-ad-id]',
        contentSelector: undefined, // rename to pageFragment
        binder: $(window),          // Cache reference to selector.

        // Positioning params.
        animate: false,             // Use smooth scrolling to ease in the new content.
        bufferPx: 40,               // Add extra height to distance remaining in the scroll area. Used when calculating trigger for next page load.
        extraScrollPx: 150,         // Add extra height when smooth scrolling in new content.
        pixelsFromNavToBottom: undefined,   // Used when calculating trigger for next page load.
        prefill: false,             // IF the document is smaller than the window THEN load data until the document is larger OR links are exhausted.

        // Result page number params.
        path: undefined,            // Either parts of a URL as an array (e.g. ["/page/", "/"] or a function that takes the page number and returns a URL.
        pathParse: undefined,       // Callback function to parse the HREF of [Next Page] <A> element to extract the page number.
        pathMatch: false,           // Check if current browser path is same as ajax pagination path
        maxPage: undefined,         // Manually controls maximum page: (IF maxPage is undefined THEN maximum page limitation will not work).

        // AJAX params.
        appendCallback: true,       // Append next page of returned items to existing result list or not.
        dataType: 'html',           // Default datatype of fetched paged results. Values are: ()'html', 'html+callback', 'json')
        template: undefined         // IF dataType == 'json' AND appendCallback == TRUE THEN you must define this function to parse JSON to HTML.
    });
```


### Examples

### Scrolling inside an element

To scroll inside an element having `overflow`, use the `local` behavior.

```javascript
$('.selector').infinitescroll({
  behavior: 'local',
  binder: $('.selector'), // scroll on this element rather than on the window
  // other options
});
```

### Loading JSON data

As explained on the website, Infinite Scroll is designed for progressive enhancement, using existing pagination links. However, it is still possible to work with JSON data.

It means the `nextSelector` href will be called via AJAX, expecting JSON data, which will be passed to the callback function.

```javascript
$('.selector').infinitescroll({
  // other options
  dataType: 'json',
  appendCallback: false
}, function(json, opts) {
  // Get current page
  var page = opts.state.currPage;
  // Do something with JSON data, create DOM elements, etc ..
});
```

## License

The MIT License (MIT)

Copyright (c) 2014 Paul Irish

Permission is hereby granted, free of charge, to any person obtaining a copy
of this software and associated documentation files (the "Software"), to deal
in the Software without restriction, including without limitation the rights
to use, copy, modify, merge, publish, distribute, sublicense, and/or sell
copies of the Software, and to permit persons to whom the Software is
furnished to do so, subject to the following conditions:

The above copyright notice and this permission notice shall be included in
all copies or substantial portions of the Software.

THE SOFTWARE IS PROVIDED "AS IS", WITHOUT WARRANTY OF ANY KIND, EXPRESS OR
IMPLIED, INCLUDING BUT NOT LIMITED TO THE WARRANTIES OF MERCHANTABILITY,
FITNESS FOR A PARTICULAR PURPOSE AND NONINFRINGEMENT. IN NO EVENT SHALL THE
AUTHORS OR COPYRIGHT HOLDERS BE LIABLE FOR ANY CLAIM, DAMAGES OR OTHER
LIABILITY, WHETHER IN AN ACTION OF CONTRACT, TORT OR OTHERWISE, ARISING FROM,
OUT OF OR IN CONNECTION WITH THE SOFTWARE OR THE USE OR OTHER DEALINGS IN
THE SOFTWARE.
