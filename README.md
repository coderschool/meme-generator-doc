# Meme Generator App

Meme Generator is a simple website to create memes. 

## Features

* User can upload png, jpg, jpeg files (use [Multer](https://www.npmjs.com/package/multer))
* The server will resize the uploaded images to 400x400
* User can add text on the image to create memes (use [Jimp](https://www.npmjs.com/package/jimp))
* The server will store the original images and the meme (original image + text)
* User can see a list of memes made by other users

## Implementation

### Server side

* [Setup with express-generator](/doc/server/00_setup_project.md)
* [Project structure](/doc/server/01_project_structure.md)
* [Setup app.js](/doc/server/02_setup_app_js.md)
* [Setup Postman](/doc/server/03_setup_postman.md)
* [User can upload an image](/doc/server/04_upload_image.md)
* [Middleware to resize the uploaded images](/doc/server/05_resize_image.md)
* [Save meme data using controller](/doc/server/06_save_meme_data.md)
* [User can get a list of memes with pagination](/doc/server/07_meme_list.md)
* [User can see a list of original images](/doc/server/08_org_image_list.md)
* [User can edit the texts on the meme](/doc/server/09_update_meme.md)

### Client side

* [Setup a React App](/doc/client/00_setup_project.md)
* [Project Structure](/doc/client/01_project_structure.md)
* [Redux configuration](/doc/client/02_redux_config.md)
* [React Router and layouts](/doc/client/03_routes_layouts.md)
* [User can see the list of memes in gallery page with pagination](/doc/client/04_meme_list.md)
* [User can create a new meme by uploading an image](/doc/client/05_create_meme.md)
* [User can add text to the image](/doc/client/06_add_text.md)