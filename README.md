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
