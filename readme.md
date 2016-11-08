# image-to-data-uri

Tiny clientside module that takes an image url, downloads the image and creates a [data URI](https://developer.mozilla.org/en-US/docs/data_URIs) from it using a hidden canvas element.


## Why would you want this?

Say you're building a chat tool and you're showing the user's avatar with each new chat. Every time you render a new chat message you'll create a new `<img>` tag with a url for an image that you very likely already have gotten from rendering a previous chat.

The problem is, each time you create an image tag with a url the browser will make a request for fetching that image. If you already have the image... that's silly. So instead of instantly rendering the user's image with the new chat, you won't see that image until the browser's fetched the image again. You may be thinking that's dumb, just use better cache headers when serving the images, but you're missing the point. What if those are coming from a source you don't control, like gravatar.

So instead, we run it through this little tool and cache the resulting data URI as part of our model that represents that user and we're golden, then when you get a chat from that user again, you just use the data URI instead of the URL as the `src` attribute on your `<img>` tag and you'll instantly see the new chat and avatar. w00t!


## Installing

```
npm i image-to-data-uri
```

## Using

```js
var imageToURI = require('image-to-data-uri')

imageToURI('http://something.com/some-image.png', function (err, uri) {
  if (!err) {
    // cache the resulting URI on a model somewhere or
    // attach it to an <img>
    var img = document.createElement('img')
    img.src = uri
    document.body.appendChild(img)
  }
})

```

## Feedback

If you dig it, follow [@HenrikJoreteg](http://twitter.com/henrikjoreteg) on the twitterwebs. If not, file issues or send pull requests :)

## License

MIT
