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

## Workflow to automatically build and deploy 

* Add github workflow file: `.github/workflows/deploy.yml`
* Add the workflow:
```
    name: Deploy
    
    on:
      push:
        # Sequence of patterns matched against refs/heads
        branches:
          # Push events on master branch
          - master
    jobs:
      deploy:
        runs-on: ubuntu-latest
        steps:
          - uses: actions/checkout@v2
          - uses: actions/setup-node@v1
            with:
              node-version: 12
          - run: git config user.email "$GITHUB_ACTOR@users.noreply.github.com"
          - run: git config user.name "$GITHUB_ACTOR"
          - run: npm ci
          - run: npm run build
          - run: git add .
          - run: git commit -m "update docs" --allow-empty
          - run: git push "https://$GITHUB_ACTOR:$GITHUB_TOKEN@github.com/$GITHUB_REPOSITORY"
```
* Commit to github, the workflow will automatically build the project and deploy to `/docs` folder

