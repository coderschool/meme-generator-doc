## Middleware to resize the uploaded images

Let's continue to build another middleware to resize the uploaded image to have 400 pixel max width or heigth. We are using the libary Jimp.

- Create `helpers/photo.helper.js`:
  ```javascript
  const Jimp = require("jimp");
  const photoHelper = {};

  photoHelper.resize = async (req, res, next) => {
    if (req.file) {
      try {
        const image = await Jimp.read(req.file.path);
        await image.scaleToFit(400, 400).write(req.file.path);
        next();
      } catch (err) {
        next(err);
      }
    } else {
      next(new Error("Image required"));
    }
  };

  module.exports = photoHelper;
  ```
- Then in `meme.api.js`: import `photoHelper` and add `photoHelper.resize` after `uploader`:
  ```diff
  +const photoHelper = require("../helpers/photo.helper");
  ...
  router.post(
    "/",
    uploader.single("image"),
  + photoHelper.resize,
    (req, res, next) => {
      console.log(req.file);
      res.send({ status: "ok" });
    }
  );
  ```

### Evaluation

- Test again with the Postman request `Create meme`
- You should see that the image that is saved in `public/images` is now resized.

Good job! [Back to instructions](/README.md)
