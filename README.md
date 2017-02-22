# BlueCompute Web Application by IBM Cloud

*This project is part of the 'IBM Cloud Native Reference Architecture' suite, available at
https://github.com/ibm-cloud-architecture/refarch-cloudnative*

The BlueCompute Web application is built to demonstrate how to access the Omnichannel APIs hosted on IBM Cloud. The application provides the basic function to allow user to browse the Catalog items, make an Order and submit review comments. The Web application is built with AngularJS in Web 2.0 Single Page App style. It uses a Node.js backend to host the static content and implement the BFF (Backend for Frontend) pattern.

## Run the Web application locally

1. Navigate to the web app folder `StoreWebApp` in the git repository.
2. Edit the config/default.json file to configure the API endpoints. You need to update following fields:
  - client_id
  - host  
  - org  
  - catalog  

  You can get these information from your API Connect management console. Click on the "BlueCompute" catalog, then navigate to **Settings -> Endpoints** tab. You will find the API Base URL. It is in the format of **https://[host]/[org]/[catalog]**. Catalog should always be "bluecompute" in this case.
  
  You need to make sure the setting `local_mode` is set as `true` when testing locally.

  ![Web App Configuration](static/imgs/bluecompute_config.png?raw=true)

3. Run the Web application

  The application uses [Bower](https://bower.io/) to manage the dependencies for Web front end library like AngularJS. You need to install all the dependencies first:
  
   `$ cd StoreWebApp`
   `$ cd public/resources`
   `$ bower install`
  
    Now, you can prepare the Node.js BFF modules and run the application
     
   `$ cd ../..`
   `$ npm install`  
   `$ npm start`  

   This will start the Node.js application on your local environment and open a browser with app homepage.

4. Validate the application.

   The application is lunched in a browser at:

   [http://127.0.0.1:8000/](http://127.0.0.1:8000/)
   
  ![BlueCompute List](static/imgs/bluecompute_web_home.png?raw=true)

  Click the "Browse Item Catalog" will load the list of items:

  ![BlueCompute Detail](static/imgs/bluemix_25.png?raw=true)
  
  Click on one of the items will bring you to the detail page. 

Feel free to play around and explore the Web application.

## Deploy the application to Bluemix hosting:

You can deploy the application to your Bluemix environment using the automated DevOps open toolchain or manually if you would like to get familiar with how to operate in Bluemix. 

### Deploy using Bluemix DevOps Continuous Delivery Toolchain

Click the button below will create the automated DevOps open toolchain in your environment and kick off the deployment. 

[![bluecompute-web-toolchain](https://new-console.ng.bluemix.net/devops/graphics/create_toolchain_button.png)](https://new-console.ng.bluemix.net/devops/setup/deploy/?repository=https://github.com/ibm-cloud-architecture/refarch-cloudnative-bluecompute-web.git&branch=master)

### Deploy using Bluemix CLI
You need to have Bluemix command line (bx or cf) installed, as well as Node.js runtime in your development environment.

- Configure the application

  You need to change the `config\default.json` configuration to inform application is running in Bluemix by change the setting  `local_mode` to `false` before deployment.

  You need to change the Cloud Foundry application route for your own web application hostname. Edit the `StoreWebApp/manefest.yml` file to update the name and host fields:

  ```yml
  applications:
  - path: .
    memory: 256M
    instances: 1
    domain: mybluemix.net
    name: bluecompute-web-app
    host: bluecompute-web-app
    disk_quota: 1024M
  ```

  Replace the `bluecompute-web-app` with your own application host name for example: `bluecompute-web-app-firstname-lastname-date`.

- Deploy the application:

  `$ cd StoreWebApp`  
  `$ cf login`  
  `$ cf push`   

Replace the {your_app_host_name} with your unique application name on Bluemix.

- Validate the application:

Once the application is deployed successfully to Bluemix, you can browse your Web app at:

[http://bluecompute-web-app.mybluemix.net/](http://bluecompute-web-app.mybluemix.net)
