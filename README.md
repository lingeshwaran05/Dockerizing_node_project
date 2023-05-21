# Dockerizing_node_project

## Prerequisites
1. Ubuntu 18.04 system with server setup
2. Docker installed on your server
3. Node.js and npm installed
4. A Docker Hub account. For storing files and fetch , pull , push like github

## Step 1 — Installing Your Project Dependencies
1. Create a directory for the project ```mkdir node_project```
2. Navigate  to the directory ```cd node_project```
3. create a package.json file with project’s dependencies ```nano package.json```
4. add dependencies into package.json file 
```
{
  "name": "nodejs-image-demo",
  "version": "1.0.0",
  "description": "nodejs image demo",
  "author": "Sammy the Shark <sammy@example.com>",
  "license": "MIT",
  "main": "app.js",
  "keywords": [
    "nodejs",
    "bootstrap",
    "express"
  ],
  "dependencies": {
    "express": "^4.16.4"
  }
}
```
5. install project’s dependencies ```npm install```
 
## Step 2 — Creating the Project Files
1. create app.js file ```nano app.js```
2. add the Express application and Router objects and define the base directory and port as constants:
```
const express = require('express');
const app = express();
const router = express.Router();

const path = __dirname + '/views/';
const port = 8080;

router.use(function (req,res,next) {
  console.log('/' + req.method);
  next();
});

router.get('/', function(req,res){
  res.sendFile(path + 'index.html');
});

router.get('/sharks', function(req,res){
  res.sendFile(path + 'sharks.html');
});

app.use(express.static(path));
app.use('/', router);

app.listen(port, function () {
  console.log('Example app listening on port 8080!')
})
```

### step 3 add our project file that is static webpage html and css files

1. create views folder ```mkdir views```
2. create ```index.html``` file ```nano views/index.html```
3. Fill the content with below code
```
<!DOCTYPE html>
<html lang="en">

<head>
    <title>About Sharks</title>
    <meta charset="utf-8">
    <meta name="viewport" content="width=device-width, initial-scale=1">
    <link rel="stylesheet" href="https://stackpath.bootstrapcdn.com/bootstrap/4.1.3/css/bootstrap.min.css" integrity="sha384-MCw98/SFnGE8fJT3GXwEOngsV7Zt27NXFoaoApmYm81iuXoPkFOJwJ8ERdknLPMO" crossorigin="anonymous">
    <link href="css/styles.css" rel="stylesheet">
    <link href="https://fonts.googleapis.com/css?family=Merriweather:400,700" rel="stylesheet" type="text/css">
</head>

<body>
    <nav class="navbar navbar-dark bg-dark navbar-static-top navbar-expand-md">
        <div class="container">
            <button type="button" class="navbar-toggler collapsed" data-toggle="collapse" data-target="#bs-example-navbar-collapse-1" aria-expanded="false"> <span class="sr-only">Toggle navigation</span>
            </button> <a class="navbar-brand" href="#">Everything Sharks</a>
            <div class="collapse navbar-collapse" id="bs-example-navbar-collapse-1">
                <ul class="nav navbar-nav mr-auto">
                    <li class="active nav-item"><a href="/" class="nav-link">Home</a>
                    </li>
                    <li class="nav-item"><a href="/sharks" class="nav-link">Sharks</a>
                    </li>
                </ul>
            </div>
        </div>
    </nav>
    <div class="jumbotron">
        <div class="container">
            <h1>Want to Learn About Sharks?</h1>
            <p>Are you ready to learn about sharks?</p>
            <br>
            <p><a class="btn btn-primary btn-lg" href="/sharks" role="button">Get Shark Info</a>
            </p>
        </div>
    </div>
    <div class="container">
        <div class="row">
            <div class="col-lg-6">
                <h3>Not all sharks are alike</h3>
                <p>Though some are dangerous, sharks generally do not attack humans. Out of the 500 species known to researchers, only 30 have been known to attack humans.
                </p>
            </div>
            <div class="col-lg-6">
                <h3>Sharks are ancient</h3>
                <p>There is evidence to suggest that sharks lived up to 400 million years ago.
                </p>
            </div>
        </div>
    </div>
</body>

</html>
```
4. create a another HTML file for navigation ```nano views/sharks.html```
5. add the below code to sharks.html 
```
<!DOCTYPE html>
<html lang="en">

<head>
    <title>About Sharks</title>
    <meta charset="utf-8">
    <meta name="viewport" content="width=device-width, initial-scale=1">
    <link rel="stylesheet" href="https://stackpath.bootstrapcdn.com/bootstrap/4.1.3/css/bootstrap.min.css" integrity="sha384-MCw98/SFnGE8fJT3GXwEOngsV7Zt27NXFoaoApmYm81iuXoPkFOJwJ8ERdknLPMO" crossorigin="anonymous">
    <link href="css/styles.css" rel="stylesheet">
    <link href="https://fonts.googleapis.com/css?family=Merriweather:400,700" rel="stylesheet" type="text/css">
</head>
<nav class="navbar navbar-dark bg-dark navbar-static-top navbar-expand-md">
    <div class="container">
        <button type="button" class="navbar-toggler collapsed" data-toggle="collapse" data-target="#bs-example-navbar-collapse-1" aria-expanded="false"> <span class="sr-only">Toggle navigation</span>
        </button> <a class="navbar-brand" href="/">Everything Sharks</a>
        <div class="collapse navbar-collapse" id="bs-example-navbar-collapse-1">
            <ul class="nav navbar-nav mr-auto">
                <li class="nav-item"><a href="/" class="nav-link">Home</a>
                </li>
                <li class="active nav-item"><a href="/sharks" class="nav-link">Sharks</a>
                </li>
            </ul>
        </div>
    </div>
</nav>
<div class="jumbotron text-center">
    <h1>Shark Info</h1>
</div>
<div class="container">
    <div class="row">
        <div class="col-lg-6">
            <p>
                <div class="caption">Some sharks are known to be dangerous to humans, though many more are not. The sawshark, for example, is not considered a threat to humans.
                </div>
                <img src="https://assets.digitalocean.com/articles/docker_node_image/sawshark.jpg" alt="Sawshark">
            </p>
        </div>
        <div class="col-lg-6">
            <p>
                <div class="caption">Other sharks are known to be friendly and welcoming!</div>
                <img src="https://assets.digitalocean.com/articles/docker_node_image/sammy.png" alt="Sammy the Shark">
            </p>
        </div>
    </div>
</div>

</html>
```
6. now add css files ```mkdir views/css```
7. create styles css file ```nano views/css/styles.css``` and add the below content
```
.navbar {
	margin-bottom: 0;
}

body {
	background: #020A1B;
	color: #ffffff;
	font-family: 'Merriweather', sans-serif;
}

h1,
h2 {
	font-weight: bold;
}

p {
	font-size: 16px;
	color: #ffffff;
}

.jumbotron {
	background: #0048CD;
	color: white;
	text-align: center;
}

.jumbotron p {
	color: white;
	font-size: 26px;
}

.btn-primary {
	color: #fff;
	text-color: #000000;
	border-color: white;
	margin-bottom: 5px;
}

img,
video,
audio {
	margin-top: 20px;
	max-width: 80%;
}

div.caption: {
	float: left;
	clear: both;
}
```
## step 4 Run the project locally

1. Navigate to project’s root directory ```cd /node_project```
2. start the application ```node app.js```
3. Application is running on port  ```http://127.0.0.1:8080/```
4. terminal output ```Example app listening on port 8080!```

![image](https://github.com/lingeshwaran05/Dockerizing_node_project/assets/76167753/a8c2137d-406f-4604-b436-cb1209b88efe)

![image](https://github.com/lingeshwaran05/Dockerizing_node_project/assets/76167753/de088e3c-a66f-4163-a3bf-dc2b95e069c8)


## Step 5 — Writing the Dockerfile
 
1. create the Dockerfile in root directory ```nano Dockerfile```
2. set the base image , here we are using alphine because it is smaller
```FROM node:10-alpine```
3. instead of running in root directory we make non root node user to run the project without any dependencies and giving all permissions to the directory
```RUN mkdir -p /home/node/app/node_modules && chown -R node:node /home/node/app```
4. create a working directory ```WORKDIR /home/node/app```
5. copy package.json dependancies to the current working directory ```COPY package*.json ./```
6. create a node user ```USER node```
7. main part code to run out node project ```RUN npm install```
8. copy application code with the appropriate permissions to the application directory on the container ```COPY --chown=node:node . . ```
9. set the port on the container  to start the project 
```EXPOSE 8080

CMD [ "node", "app.js" ]
```
overall code :

```
FROM node:10-alpine

RUN mkdir -p /home/node/app/node_modules && chown -R node:node /home/node/app

WORKDIR /home/node/app

COPY package*.json ./

USER node

RUN npm install

COPY --chown=node:node . .

EXPOSE 8080

CMD [ "node", "app.js" ]
```

## step 6 - build the docker image 

1. ```docker build -t your_dockerhub_username/nodejs-image-demo .```
2. ![image](https://github.com/lingeshwaran05/Dockerizing_node_project/assets/76167753/dc4fa989-1d54-45ac-a183-3be636be7569)

3. ```docker images```

newly created Docker image

![image](https://github.com/lingeshwaran05/Dockerizing_node_project/assets/76167753/b7d00b5c-7c37-4e1a-82bb-6d831ee9fdb8)


4. Our newly created docker image will be on Docker desktop in ```unused state```


![image](https://github.com/lingeshwaran05/Dockerizing_node_project/assets/76167753/5bb2c1f3-c487-4cd0-b7c7-4babff79b17a)



5. Now we can run the docker image with ```docker run --name nodejs-image-demo -p 80:8080 -d your_dockerhub_username/nodejs-image-demo``` or run it manually in docker desktop environment


![image](https://github.com/lingeshwaran05/Dockerizing_node_project/assets/76167753/30799d38-9d7b-4139-9ee2-b52a2926e6f9)


6. view the docker process 



![image](https://github.com/lingeshwaran05/Dockerizing_node_project/assets/76167753/786de498-70de-4018-99e2-ea37564ab018)



7. view the webpage in ```http://127.0.0.1`` port not in ```http://127.0.0.1:8080```



![image](https://github.com/lingeshwaran05/Dockerizing_node_project/assets/76167753/0dec91a8-99b1-4375-900c-a51c6af378f5)






![image](https://github.com/lingeshwaran05/Dockerizing_node_project/assets/76167753/8b839e45-e50f-4722-8247-81f87e632c05)


![image](https://github.com/lingeshwaran05/Dockerizing_node_project/assets/76167753/2e1bd310-c8ab-4409-9e21-6b711a8b8910)



8. Now our Docker image is running which is shown in Docker Desktop


![image](https://github.com/lingeshwaran05/Dockerizing_node_project/assets/76167753/38342cb1-4116-4931-9c9b-87ae2cf25e4f)

