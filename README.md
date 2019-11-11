# hello-actions

A basic Hello World Express App to test GitHub Actions

## NPM

### Install

```
npm install
```

### Run 

```
npm start
```

### Test

```
npm test
```

### Publish

```
npm publish --dry-run
```

### ESLint 

```
npm install eslint --save-dev
./node_modules/.bin/eslint --no-eslintrc .
```

## Docker

### Build Docker container 

```
docker build --rm -f "Dockerfile" -t basp/hello-actions:latest .
```

### Run Docker container

```
docker run -d -p 8080:8080 --name hello-actions basp/hello-actions:latest
```

### Stop container

```
docker container stop hello-actions
```

### Remove container

```
docker container rm hello-actions
```

### Push to Docker Hub

```
docker push basp/hello-actions:latest
```

## Example workflow

```hcl
workflow "Build, Test and Publish" {
  on = "push"
  resolves = [
    "Publish",
    "Zeit Deploy",
    "ESLint",
  ]
}

action "Build" {
  uses = "actions/npm@59b64a598378f31e49cb76f27d6f3312b582f680"
  args = "install"
}

action "Test" {
  uses = "actions/npm@59b64a598378f31e49cb76f27d6f3312b582f680"
  args = "test"
  needs = ["Build"]
}

action "Master" {
  uses = "actions/bin/filter@d820d56839906464fb7a57d1b4e1741cf5183efa"
  needs = ["Zeit Deploy"]
  args = "branch master"
}

action "Publish" {
  uses = "actions/npm@59b64a598378f31e49cb76f27d6f3312b582f680"
  needs = ["Master"]
  args = "publish --dry-run"
}

action "Zeit Deploy" {
  uses = "actions/zeit-now@666edee2f3632660e9829cb6801ee5b7d47b303d"
  needs = ["Test", "ESLint"]
  secrets = ["ZEIT_TOKEN"]
}

action "ESLint" {
  uses = "actions/npm@59b64a598378f31e49cb76f27d6f3312b582f680"
  needs = ["Build"]
  runs = "./node_modules/.bin/eslint --no-eslintrc ."
}
```
