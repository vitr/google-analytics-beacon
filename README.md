# Google Analytics Beacon ![analytics image](https://raw.githubusercontent.com/igrigorik/ga-beacon/master/static/badge-flat.gif "Analytics Image - Flat")

Sometimes it is impossible to embed the JavaScript tracking code provided by Google Analytics: the host page does not allow arbitrary JavaScript, and there is no Google Analytics integration. However, not all is lost! **If you can embed a simple image (pixel tracker), then you can beacon data to Google Analytics.**

---------------
This is tweaked version of [igrigorik/ga-beacon](https://github.com/igrigorik/ga-beacon).
As the original author suggests:
>there are no capacity or availability promises. For best results, deploy your own instance directly on Google App Engine.

Unfortunately, many people don't bother with creating  their own instances and we all see this
![over quota error image](https://github.com/vitr/vitr.github.io/blob/master/_posts/Image%201.png?raw=true "Over Quota")

This repo was created to help you with setting up your own Google Analytis Beacon application, so, you will never have availabiltiy issues like above.

Its usage is also restricted by your onw tracking ids (`UA-XXXXXXXX-X`). The file `ga-beacon/conf.json` contains a white list of allowed tracking ids. This implies, you have to update the list every time you want to track something with a new tracking id. Leave the list empty, if you don't want to restrict, but keep in mind, with no restrictions anyone can use your application instance for tracking their visitors and you may pay for that. Here an example of `ga-beacon/conf.json`

    {
        "TrackingIds": ["UA-XXXXXXXX-X","UA-YYYYYYYY-Y,"UA-ZZZZZZZZ-Z"]
    }

### How to deploy on Google App Engine
You should deploy this application on your server. Using Google App Engine is free and easiest way to do so. Be aware of GAE free usage limits https://cloud.google.com/appengine/docs/quotas#Requests. If you run over quota, you'll see the image above and lose some stats. Unless you have very popular resource or other people also use your instance for tracking (consider applying the restriction), GAE daily limits are very generous. There are two options for delpoyment on GAE:

#### Using Google Developers Console (easy)

1. Fork this repo
2. Go to https://console.cloud.google.com/
3. Create a project **My-Project**
4. Go to Development->Source code and connet the forked repo
5. cd ~/src/My-Project-ID/
6. gcloud preview app deploy app.yaml --promote 
7. see the app at https://vitr-analytics.appspot.com/UA-75628680-1/

 


#### Using Google App Engine SDK for Go (advanced)
https://cloud.google.com/appengine/downloads#Google_App_Engine_SDK_for_Go

[Hello, World! in 5 minutes - Go — Google Cloud Platform](https://cloud.google.com/appengine/docs/go/)

http://stackoverflow.com/questions/32107712/google-app-engine-app-deployment

In my case, I got refused because the appcfg save my ouauth2 token in the file ~/.appcfg_oauth2_tokens, which happen to be another account of appengine . Simply remove the file and try again.

### How to setup

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

It's useful to read the original project [FAQ](https://github.com/igrigorik/ga-beacon#faq)

### Roadmap

- [x] Modify original Go programm to optionally restrict usage by tracking id
- [ ] Add GAE deployment help
- [ ] Add setup help (update original help with recent workflow)
- [ ] Deploy on AWS Elastic Beanstalk
- [ ] Create docker image for universal deployment


