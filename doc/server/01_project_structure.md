## Project structure

In the end, your project folder will look like:

```
|- bin/
|- controllers/
    |- meme.controller.js
|- helpers/
    |- photo.helper.js
    |- upload.helper.js
    |- utils.helper.js
|- public/
    |- images/
|- routes/
    |- index.js
    |- meme.api.js
|- app.js
|- memes.json
```

- The uploaded images will be store in `public/images/`
- `memes.json` is our "database" which store data about the memes like original images, texts, etc.
- `meme.controller.js` contains handler functions that handle the requests from front-end.
- `photo.helper.js` contains helper function to resize, or put text on image.
- `upload.helper.js` is a middleware to handle uploading images.
- `routes/index.js` define all of the routes in the app. We only have a few APIs in `meme.api.js`, but it's good to follow the pattern that allows your app to scale later on.

Good job! [Back to instructions](/README.md)