# activity-mocks

Mock [JSON Activity Streams](http://tools.ietf.org/html/draft-snell-activitystreams-09) Objects you can use to develop other components.

## Using

The source is intended to be run by node (not, e.g. [cajon](https://github.com/requirejs/cajon)).

A UMD build is distributed in [dist/](./dist), and can be generated with `make dist`.

## Mocks

### From [jasnell/activitystreams.jsonld](https://github.com/jasnell/activitystreams.jsonld) README.

* [strings](./mocks/strings.json) - Has only string values for Activity properties
* [jsonld](./mocks/jsonld.json) - The 'extended example' whose .object has its own jsonld context

### From [the Spec](http://tools.ietf.org/html/draft-snell-activitystreams-09)

* [spec.minimal](./mocks/spec/minimal.json) - [Example 1: Minimal Activity](http://tools.ietf.org/html/draft-snell-activitystreams-09#section-2.1)
* [spec.basicWithDetail](./mocks/spec/basic-with-detail.json) - [Example 2: Basic activity with some additional detail](http://tools.ietf.org/html/draft-snell-activitystreams-09#section-2.2)
* [spec.extended](./mocks/spec/extended.json) - [Example 3: An extended activity](http://tools.ietf.org/html/draft-snell-activitystreams-09#section-2.3)

### Vendors

#### Livefyre

* [livefyre.sitePostCollection](./mocks/livefyre/site-post-collection.json)
* [livefyre.userPostMessage](./mocks/livefyre/user-post-message.json)

## API

The main export is a tree of the different sets of mocks

```javascript
var activityMocks = require('activity-mocks');
activityMocks.strings;
activityMocks.jsonld;
activityMocks.livefyre.userPostMessage;
activityMocks.livefyre.sitePostCollection;
```

You can create a new instance of a mock by name

```javascript
var activityMocks = require('activity-mocks');
activityMocks.create('strings');
activityMocks.create('jsonld');
activityMocks.create('livefyre.userPostMessage');
activityMocks.create('livefyre.sitePostCollection');
```

You can get an array of all mocks

```javascript
require('activity-mocks').toArray();
```

You can get a list of all names

```javascript
var activityMocks = require('activity-mocks');
activityMocks.names
  .filter(function (name) {
    return name.indexOf('livefyre.') === 0;
  })
  .map(activityMocks.create);
```

## `make` commands

* `make build` - will `npm install` and `bower install`
* `make dist` - will use r.js optimizer to compile the source, UMD wrap, and place that and source maps in dist/
* `make clean`
* `make server` - serve the repo over http
* `make deploy [env={*prod,uat,qa}]` - Deploy to lfcdn, optionally specifying a bucket env
