---
layout: post
title: "Angular Setup with ng-cli"
tags: [angular]
image:
  feature: avatar.jpg
  credit: 
  creditlink: 
comments: true
share: true
---
---
> " Children are not a distraction from more important work. They are the most important work."
---

The [Angular CLI](https://github.com/angular/angular-cli) is a command-line interface tool to setup the angular development environment and create a project with running code.

To setup the development environment,
#### Install angular-cli globally
``` 
npm install -g @angular\cli
```
#### Generate new Project
Create a new project and navigate to the project directory
```
ng new baby-app
cd baby-app
```
This step takes a little time, since it involves installing a lot of npm packages.
#### Run the application

```
ng serve --open
```

```ng serve``` will launch the server 

```--open``` or ```--o``` opens the url http://localhost:4200 in default browser

To change the default port and host, use
```
ng serve --host 0.0.0.0 --port 4201
```

To get the list of options, use
```
ng help
``` 

#### Sourcode is available [here](https://github.com/DeepikaRajendran/baby-app/tree/initial_setup)
