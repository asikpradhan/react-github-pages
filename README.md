# Host react app as github pages

* Start by bootstrapping your app with [Create React App](https://github.com/facebook/create-react-app).
* Add `rimraf` package to your project
```
     npm install rimraf --save-dev
```
* Add homepage to 'package.json' file:
```
    "homepage": "https://{username}.github.io/{repository-name}",
```
* Update build script in your package.json file:
 ```
    "prebuild": "rimraf docs",
    "build": "react-scripts build && mv build docs",
```
* Run `npm run build`
* Commit your code to github
* Setup your github pages to point to `/docs`


