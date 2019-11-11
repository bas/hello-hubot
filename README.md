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
docker build --rm -f "Dockerfile" -t hello-hubot .
```

### Run Docker container

```
docker run -d -p 8080:8080 --name hello-hubot hello-hubot:latest
```

### Stop container

```
docker container stop hello-hubot
```

### Remove container

```
docker container rm hello-hubot
```