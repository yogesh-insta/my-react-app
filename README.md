# React App + NGINX + Docker-compose + CI/CD pipeline (Travis and Github) + AWS ElasticBeanStalk

**Stack:** React, NGINX, Docker Compose, Travis CI, Elastic Beanstalk

**Skills:** Containerized frontends, CI/CD


### create react application using following command 

`npx create-react-app my-react-app`

## build docker image 
`docker build -t yogeshnm/my-react-app .`

## run docker image 
docker run -p 3000:3000 yogeshnm/my-react-app

## run docker image with volume mapped to the local source folder 
`docker run -p 3000:3000 -v /app/node_modules -v $(pwd):/app yogeshnm/my-react-app`

> create reference too all local folders under current directory except node_modules.
> doing so, You can modify your code and see the changes immediately
> Alternatively we can achieve the same thing using docker-compose.yaml

`docker-compose up`

## run in production env
In production environment, we just a need bundled static files
The Dockerfile for production contain two phases
1. Build you application 
2. Docker image from NGINX that consist of following two steps 
 - Create NGINX image and copy the bundled files to it!
 - start NGINX server 

> created a Dockerfile for production /Dockerfile

`docker build -t yogeshnm/my-react-app-prod .`

`docker run -p 8080:80 yogeshnm/my-reach-app-prod`

> 80 is the default port for NGINX

**Access application at http://locahost:8080**

## create CI-CD pipeline with Travis and AWS 

### create .travis.yml 
> note that .travis.yaml will result in `rake aborted!` error!

### sign-up at travis-ci.com with github account
Configure your github repository 
Whenever you create a pull request and merge the branch to master, the build and deployment will be triggered

> At this point, you can have everything in travis.yml except deploy tag and test the travis integration

### create Elastic Beanstalk application from AWS console
**Select**
   
    - create environment
    - web server env
    - platform: docker
    - sample application
    
> Elastic Beanstalk add load balancer and scales the application if required
> You will get an url something like http://myreactapp-env.eba-cp392jbp.ap-southeast-2.elasticbeanstalk.com/

### create IAM user 
 - should have a policy having full access to ElasticBeanStalk
> note down use access key and secret key

### create environment variables from Travis settings
 - use these variables in .travis.yml 

Here you should be able to see your application 
> http://myreactapp-env.eba-cp392jbp.ap-southeast-2.elasticbeanstalk.com/

### Delete AWS resources 
- navigate to Elastic Beanstalk and delete the application

### To redeploy the application 
 - create Elastic Beanstalk 
 - update relevant variables under deploy section from AWS console 


=========================================
### Following contents are part of the project created from command line, keeping it here for reference
This project was bootstrapped with [Create React App](https://github.com/facebook/create-react-app).

## Available Scripts

In the project directory, you can run:

### `npm start`

Runs the app in the development mode.<br />
Open [http://localhost:3000](http://localhost:3000) to view it in the browser.

The page will reload if you make edits.<br />
You will also see any lint errors in the console.

### `npm test`

Launches the test runner in the interactive watch mode.<br />
See the section about [running tests](https://facebook.github.io/create-react-app/docs/running-tests) for more information.

### `npm run build`

Builds the app for production to the `build` folder.<br />
It correctly bundles React in production mode and optimizes the build for the best performance.

The build is minified and the filenames include the hashes.<br />
Your app is ready to be deployed!

See the section about [deployment](https://facebook.github.io/create-react-app/docs/deployment) for more information.

### `npm run eject`

**Note: this is a one-way operation. Once you `eject`, you can’t go back!**

If you aren’t satisfied with the build tool and configuration choices, you can `eject` at any time. This command will remove the single build dependency from your project.

Instead, it will copy all the configuration files and the transitive dependencies (webpack, Babel, ESLint, etc) right into your project so you have full control over them. All of the commands except `eject` will still work, but they will point to the copied scripts so you can tweak them. At this point you’re on your own.

You don’t have to ever use `eject`. The curated feature set is suitable for small and middle deployments, and you shouldn’t feel obligated to use this feature. However we understand that this tool wouldn’t be useful if you couldn’t customize it when you are ready for it.

## Learn More

You can learn more in the [Create React App documentation](https://facebook.github.io/create-react-app/docs/getting-started).

To learn React, check out the [React documentation](https://reactjs.org/).

### Code Splitting

This section has moved here: https://facebook.github.io/create-react-app/docs/code-splitting

### Analyzing the Bundle Size

This section has moved here: https://facebook.github.io/create-react-app/docs/analyzing-the-bundle-size

### Making a Progressive Web App

This section has moved here: https://facebook.github.io/create-react-app/docs/making-a-progressive-web-app

### Advanced Configuration

This section has moved here: https://facebook.github.io/create-react-app/docs/advanced-configuration

### Deployment

This section has moved here: https://facebook.github.io/create-react-app/docs/deployment

### `npm run build` fails to minify

This section has moved here: https://facebook.github.io/create-react-app/docs/troubleshooting#npm-run-build-fails-to-minify
