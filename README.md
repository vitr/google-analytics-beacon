# Google analytics Beacon
This is tweaked version of [igrigorik/ga-beacon](https://github.com/igrigorik/ga-beacon).
As the original author suggests:
>there are no capacity or availability promises. For best results, deploy your own instance directly on Google App Engine.

This repo is created with that idea in mind. Its usage is also restricted by your onw tracking ids (`UA-XXXXX-X`). The file `ga-beacon/conf.json` contains a white list of allowed tracking ids. This implies, you have to update the list everytime you want to track something with a new tracking id (`UA-XXXXX-X`). Leave the list empty, if you don't want to restrict, but keep in mind, with no restrictions anyone can use your application instance for tracking their visitors and you may pay for that.



http://stackoverflow.com/questions/32107712/google-app-engine-app-deployment

In my case, I got refused because the appcfg save my ouauth2 token in the file ~/.appcfg_oauth2_tokens, which happen to be another account of appengine . Simply remove the file and try again.
