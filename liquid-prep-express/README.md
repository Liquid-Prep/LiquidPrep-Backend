# [Liquid Prep - App](https://liquid-prep-app.s3-web.us-east.cloud-object-storage.appdomain.cloud/)

[![Click](https://img.shields.io/badge/Click-Liquid%20%20Prep%20App-blue)](https://liquid-prep-app.s3-web.us-east.cloud-object-storage.appdomain.cloud/)

Liquid Prep App is an user interface that is accessed on your mobile device to get water advise for the selected crop. It is a [Progressive Web App (PWA)](https://web.dev/progressive-web-apps/) developed with [Angular](https://angular.io/) web framework.

The Liquid Prep App gets the Weather and Crops data from the [Liquid Prep Backend](https://github.com/Liquid-Prep/LiquidPrep-Backend) service and the soil moisture data from the [Liquid Prep Hardware](https://github.com/Liquid-Prep/LiquidPrep-Hardware). After analysis of the weather, crop and soil moisture data the app computes and provides water advise for the selected crop.

The Liquid Prep Express App can be used for local development and be containerized (frontend and backend) as a service to run on these supported architectures: arm, arm64, x86, risk-v. This envirnoment is setup to take advantage of Open Horizon Edge Computing Management Platform to perform CI/CD deployment and continuous updates of ML models and other assets for the running applications on these edge devices.  For more information, visitt [Open Horizon](https://github.com/open-horizon)     


## Get Started

Instructions on how to run the App,

- [Pre-requisites](#pre-requisites)
- [Run App Locally](#run-app-locally)
- [Configure and Deploy App in IBM Cloud Object Storage](#configure-and-deploy-app-in-ibm-cloud-object-storage)
- [Contributing](#contributing)

### Pre-requisites

1. Node and NPM:
   - [Install Node and NPM](https://docs.npmjs.com/downloading-and-installing-node-js-and-npm)
2. Angular CLI
   - [Install Angular CLI](https://cli.angular.io/)
3. Git:
   - [Install Git](https://git-scm.com/book/en/v2/Getting-Started-Installing-Git/)
   - [Configure Git](https://git-scm.com/book/en/v2/Getting-Started-First-Time-Git-Setup)
   - [Git account setup and configuration](https://git-scm.com/book/en/v2/GitHub-Account-Setup-and-Configuration)
4. Liquid Prep project:
   - [Git clone Liquid Prep project](https://github.com/Liquid-Prep/Liquid-Prep)
5. IBM Cloud account:
   - [Create an IBM Cloud account](https://cloud.ibm.com/registration)
6. Liquid Prep Backend Service Endpoint:
   - [Deploy Liquid Prep Backend in IBM Cloud Functions](https://github.com/Liquid-Prep/Liquid-Prep/tree/master/backend#deploy-liquid-prep-backend-service) and note down the `CLOUD_FUNCTIONS_URL` which is the Backend service endpoint. This endpoint will be required later for deploying the App.

### Run App Locally

1. **Build the App**

   - Start a terminal/CMD in `LiquidPrep-App/liquid-prep-app` folder.
   - Run `npm install`.

2. **Config.json**

   - In the `LiquidPrep-App/liquid-prep-app/src/` folder, rename the file `config-sample.json` to `config.json`.
   - Update the `config.json` with Liquid Prep Backend Service Endpoint noted down in the [Pre-requisites](#pre-requisites) 6th point.

3. **Run the Apps**

   - In `LiquidPrep-App/liquid-prep-app` Run `npm run watch:deploy` to watch and hot deploy liquid-prep-app aka `frontend`.
   - In `LiquidPrep-App/liquid-prep-express` Run `npm run watch:deploy` to watch and hot reload liquid-prep-expres aka `backend`
   - Open the browser and enter `http://localhost:0000/`. The app will automatically reload if you change any of the source files.

### To containerize the application and deploy it through Open Horizon

1. Setup up local environment with the following script, this will install/setup Open Horizon and [hzn-cli](https://github.com/playground/hzn-cli) npm package   
   - Run `curl -sSL https://raw.githubusercontent.com/playground/hzn-cli/main/install.sh --output install.sh && bash ./install.sh`


Please follow the step wise instructions in the [IBM Cloud Deployment Documentation](IBM-CLOUD-SETUP.md).

## Contributing

Please read [CONTRIBUTING.md](https://github.com/Liquid-Prep/Liquid-Prep/blob/main/CONTRIBUTING.md) for details on our code of conduct, areas where we'd like to see community contributions, and the process for submitting pull requests to the project.

## License

Unless otherwise noted, this project is licensed under the Apache 2 License - see the [LICENSE](https://github.com/Liquid-Prep/Liquid-Prep/blob/main/LICENSE) file for details.
