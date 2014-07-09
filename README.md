IE-Warning-Bar
==============

Display an upgrade message to users using older versions of IE. 

This is a working example of using a couple of excellent jQuery libraries ([Bowser](https://github.com/ded/bowser) and [jQuery Cookie](https://github.com/carhartl/jquery-cookie)) to display a warning/upgrade bar to your website users that provides upgrade links for IE (boo), Firefox, Chrome and Safari.

It uses a cookie to store whether or not the user has dismissed the upgrade notice, so your users aren't spammed by the bar showing on every page load.

* * *

### Required Libraries

**[jQuery](http://jquery.com/) (cdn included in example)**

**[Bowser](https://github.com/ded/bowser) (included)**
A Browser detector. Because sometimes, there is no other way, and not even good modern browsers always provide good feature detection mechanisms.

**[jQuery Cookie](https://github.com/carhartl/jquery-cookie) (included)**
A simple, lightweight jQuery plugin for reading, writing and deleting cookies.

### How To Use
As long as you have the above JavaScript libraries included (which come as part of this repo) you will just need to copy the banner markup from the example index.html file: 

```
<!-- This is the notification bar you want in your markup at the top of the screen -->
<div id="ieMessage" style="display:none;">
    <div class="inner">
        <span class="outOfDate">Did you know your browser is out of date?</span>
        <p>To get the best possible experience using our website we recommmend that you upgrade to a newer version or other web browser. IE8 is no longer supported. A list of the most popular web browsers can be found below. Click on the links to get to the download page.</p>
        <ul>
            <li><a href="http://windows.microsoft.com/en-US/internet-explorer/downloads/ie" target="_blank">Internet Explorer</a></li>
            <li><a href="http://www.mozilla.org/en-US/" target="_blank">Firefox</a></li>
            <li><a href="http://support.apple.com/downloads/#safari" target="_blank">Safari</a></li>
            <li><a href="https://www.google.com/chrome" target="_blank">Chrome</a></li>
        </ul>
        <a class="close"></a>
    </div>
</div>
```

Then include the JavaScript from the example: 

```
<!-- This is the JS that handles the IE warning message  -->
<script>
$(document).ready(function() {

    // IE warning message - Show if using below IE9
    var ieMessage = $("#ieMessage");
    if (bowser.msie && bowser.version < 9) { // <- Change to whatever IE version you want
        if (typeof $.cookie("ieMessage") == "undefined") {
            ieMessage.slideDown(500);
        }
    }

    // Close button handler. Set a cookie so we don't show the banner on 
    // every page load.
    $("a.close", ieMessage).click(function(e) {
        e.preventDefault();
        $.cookie('ieMessage', true, { expires: 7, path: '/' });
        ieMessage.slideUp(500);
    });
});
</script>
```

Then it'll work!
