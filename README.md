# New Vue2 project process

## Define docker container

In your project folder, create a file named __docker-compose.yml__:

```
version: "3.4"
services:
  my_frontend:
    container_name: my_frontend
    image: node:lts
    working_dir: /var/www/html/app/
    entrypoint: /bin/bash
    ports:
      - "8080:8080"
    volumes:
      - ./frontend/:/var/www/html/app
    tty: true
```

## Running container

I'm spinning the container up with:

`$ docker-compose up -d`

and hooking into the container with:

`$ docker-compose exec my_frontend bash`

## Running project

### New Vue project from scratch

When in the docker container, install dependecies:

#### Vue 2

Vue.js v2.6 is required, v2.6.12 is recommended

`$ npm init vue@2.6.12`

#### Pooper


`$ npm i @popperjs/core`

#### Bootstrap 4

Bootstrap v4.3.1 is required, v4.6.1 is recommended

`$ npm i bootstrap@4.6.1`

Popper.js v1.16 is required for dropdowns (and components based on dropdown), tooltips, and popovers. v1.16.1 is installed with Bootstrap

#### PortalVue

PortalVue v2.1 is required by Toasts, v2.1.7 is recommended

`$ npm i portal-vue@2.1.7`

#### Bootstrap-Vue

Finally, install bootstrap-vue

`$ npm install bootstrap-vue`

### Create project

Install Vue

`$ npm install -g @vue/cli`

Create new project

`$ vue create .`

Then select the Vue, name the project and so on.

### Initialize project

After the project is generated, install the packages.

`$ npm install`

We can check code style 

`$ npm run lint`

### Setting up the Project for running under the Docker

#### Folder and files permissions

Change main folder permissions (in main root, out of docker instances):

`$ sudo chown <your_user>:<your_user> frontend/`

Change folder and files permissions:

`$ sudo chown -R <your_user>:<your_user> frontend/public/ frontend/src/`
`$ sudo chown <your_user>:<your_user> frontend/.gitignore frontend/babel.config.js frontend/jsconfig.json frontend/package.json frontend/README.md frontend/vue.config.js`


#### Setting up

For running the project under the Docker:

`$ npm run serve`

And that's it!

The vue application is accesible from __http://localhost:8080/__

Sometimes it is necessary to delete the __node_modules/__ directory and re-install the dependencies with:

`$ npm install`

### References

- [BootstrapVue - Getting Started](https://bootstrap-vue.org/docs)
- [Getting started with BootstrapVue](https://blog.logrocket.com/getting-started-bootstrapvue/#getting-started)
