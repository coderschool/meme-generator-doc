## User can upload an image

In this step we allow user to upload an image to the server. The server will save the image in the folder `public/images/.

- Create `/helpers/upload.helper.js`. This is a function that returns the `multer` middleware to save the image. The function takes in a folder path, create the folder if it's not exists, and use it as the storage.
  ```javascript
  const fileUploadHelper = (filePath) => {
  const multer = require("multer");
  const path = require("path");
  const mkdirp = require("mkdirp");

  const storage = multer.diskStorage({
    destination: async (req, file, cb) => {
      const uploadPath = path.resolve(filePath);
      try {
        const folderStat = await ensureFolderExists(uploadPath);
        if (folderStat) {
          cb(null, uploadPath);
        } else {
          cb(null, "");
        }
      } catch (err) {
        cb(err);
      }
    },
    filename: function (req, file, cb) {
      const uniquePrefix = Date.now() + "-" + Math.round(Math.random() * 1e9);
      cb(null, uniquePrefix + "-" + file.originalname);
      },
    });
    const ensureFolderExists = (path) => {
      return new Promise((resolve, reject) => {
        mkdirp(path, (err) => {
          if (err) {
            reject(err); // something else went wrong
          } else {
            resolve(true); // successfully created folder
          }
        });
      });
    };
    return {
      uploader: multer({
        storage: storage,
        fileFilter: (req, file, cb) => {
          if (
            !file.mimetype.includes("jpeg") &&
            !file.mimetype.includes("jpg") &&
            !file.mimetype.includes("png")
          ) {
            return cb(null, false, new Error("Only images are allowed"));
          }
          cb(null, true);
        },
      }),
    };
  };
  module.exports = fileUploadHelper;
  ```

- In `meme.api.js`:
  ```javascript
  //...
  const fileUpload = require("../helpers/upload.helper")("public/images/");
  const uploader = fileUpload.uploader;
  //...
  /**
  * @route POST api/memes
  * @description Create a new meme
  * @access Public
  */
  router.post("/", uploader.single("image"), (req, res, next) => {
    console.log(req.file);
    res.send({ status: "ok" });
  });
  ```

### Evaluation

- Open Postman, create a new POST Request to `{{url}}/api/memes` called `Create meme`. In the `body` tab, choose `form-data`, put `image` as type `file` AS `KEY`, and select a file as VALUE. Click `Send`.
  ![](./images/400_pm_create_meme.png)

- You should see the `ok` response and find the image in `public/images`. In the server console log, you should see the file object in `req` like this:
  ```
  {
    fieldname: 'image',
    originalname: 'EAb16qe3IE.jpg',
    encoding: '7bit',
    mimetype: 'image/jpeg',
    destination: 'path_to_your_project/public/images',
    filename: '1601882144635-695960738-EAb16qe3IE.jpg',
    path: 'path_to_your_project/public/images/1601882144635-695960738-EAb16qe3IE.jpg',
    size: 30894
  }
  POST /api/memes/ 200 2705.523 ms - 15
  ```

Good job! [Back to instructions](/README.md)