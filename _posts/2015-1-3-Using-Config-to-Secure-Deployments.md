---
layout: post
title: Using Config in your Workflow
---

##What is Config?
[Config](https://www.npmjs.com/package/config) is a NPM package that basically allows you to store configuration parameters in a separate file, and respond appropriately for different environments, such as staging, test, and production.

One it's many uses is the ability to obscure your application's sensitive parameters (database logins, API keys, backend addresses), as you can store all sensitive information in the config file, and then use .gitignore to not track it. This way you can still run your code base as a working local server, and still commit all changes, but your sensitive information is never publically viewable!

##Using Config
Config accepts multiple formats, but let's use JSON, which I found the easiest to use, in my opinion. 

First install config, if you haven't: `npm install config --save`

Here's the basic structure for an API key config file:

```
config/default.json

{
  // API Keys
  "APIKeys": {
    "Google": {
      "key": "abc123"
    },
    "Yahoo": {
      "key": "xyz456"
    }
  }
}
```

We can then pull the data from the config file thusly:

```
//First require the module
var config = require('config');
//Then pull the data from the file, and store it in a variable!
var googleAPIKey = config.get('APIKeys.Google.key');
var yahooAPIKey = config.get('APIKeys.Yahoo.key');
```

Don't forget to add your config file to `.gitignore`!
e.g.
```
*.log
node_modules/
config/
```

##Easy peasy!
Using config is easy! The JSON structure is very flexible. You can create custom JSON objects as you like, and traverse that object using simple dot notation in a string you pass to config.get().

Have fun!