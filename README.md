# Google Analytics Beacon ![analytics image](https://raw.githubusercontent.com/igrigorik/ga-beacon/master/static/badge-flat.gif "Analytics Image - Flat")
This is tweaked version of [igrigorik/ga-beacon](https://github.com/igrigorik/ga-beacon).
As the original author suggests:
>there are no capacity or availability promises. For best results, deploy your own instance directly on Google App Engine.

Unfortunately, many people don't bother with creating  their own instances and we all see this

![over quota image](https://github.com/vitr/vitr.github.io/blob/master/_drafts/Image%201.png?raw=true "Over Quota")

This repo was created to help you with setting up your own Google Analytis Beacon application, so, you will never have availabiltiy issues like above.

Its usage is also restricted by your onw tracking ids (`UA-XXXXXXXX-X`). The file `ga-beacon/conf.json` contains a white list of allowed tracking ids. This implies, you have to update the list everytime you want to track something with a new tracking id. Leave the list empty, if you don't want to restrict, but keep in mind, with no restrictions anyone can use your application instance for tracking their visitors and you may pay for that. Here an example of `ga-beacon/conf.json`

    {
        "TrackingIds": ["UA-XXXXXXXX-X","UA-YYYYYYYY-Y,"UA-ZZZZZZZZ-Z"]
    }



### How to deploy
1. Using Google Developers Console https://console.cloud.google.com/ (easy)
2. Using Google App Engine SDK for Go https://cloud.google.com/appengine/downloads#Google_App_Engine_SDK_for_Go (advanced)

http://stackoverflow.com/questions/32107712/google-app-engine-app-deployment

In my case, I got refused because the appcfg save my ouauth2 token in the file ~/.appcfg_oauth2_tokens, which happen to be another account of appengine . Simply remove the file and try again.

It's useful to read the original project [FAQ](https://github.com/igrigorik/ga-beacon#faq)
---------------
Sometimes it is impossible to embed the JavaScript tracking code provided by Google Analytics: the host page does not allow arbitrary JavaScript, and there is no Google Analytics integration. However, not all is lost! **If you can embed a simple image (pixel tracker), then you can beacon data to Google Analytics.** For a great, hands-on explanation of how this works, check out the following guides:

* [Using a Beacon Image for GitHub, Website and Email Analytics](http://www.sitepoint.com/using-beacon-image-github-website-email-analytics/)
* [Tracking Google Sheet views with Google Analytics using GA Beacon](http://mashe.hawksey.info/2014/02/tracking-google-sheet-views-with-google-analytics/)

### Setup instructions

First, log in to your Google Analytics account and [set up a new property](https://support.google.com/analytics/answer/1042508?hl=en):

* Select "Website", use new "Universal Analytics" tracking
* **Website name:** anything you want (e.g. GitHub projects)
* **WebSite URL: https://ga-beacon.appspot.com/**
* Click "Get Tracking ID", copy the `UA-XXXXX-X` ID on next page

Next, add a tracking image to the pages you want to track:

* _https://ga-beacon.appspot.com/UA-XXXXX-X/insert/any/path_
* `UA-XXXXX-X` should be your tracking ID
* `insert/any/path` is an arbitrary path. For best results specify a meaningful and self-descriptive path. You have to do this manually, the beacon won't automatically record the page path it's embedded on.

Example tracker markup if you are using Markdown:

```markdown
[![Analytics](https://ga-beacon.appspot.com/UA-XXXXX-X/welcome-page)](https://github.com/igrigorik/ga-beacon)
```


If you prefer, you can skip the badge and use a transparent pixel. To do so, simply append `?pixel` to the image URL. There are also "flat" style variants available, which are available when appending `?flat` or `?flat-gif` to the image URL. And that's it, add the tracker image to the pages you want to track and then head to your Google Analytics account to see real-time and aggregated visit analytics for your projects!
