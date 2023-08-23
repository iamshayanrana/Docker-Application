# Docker-Application

## Combined Environment Docker Project

In this project we have to create a container where there is only 1 Dockerfile and 1 docker-compose.yml file in which we have to run PHP/Laravel, Vue.js, Node.js, Python. I use Docker to set this up.

### Basics

Before you start, make sure you have two things installed:

1. Docker: This is a program that helps you create and run containers.

2. Docker Compose: This tool makes managing multiple containers even simpler.

### Project Structure

Main Directory(trf) and sub directory (shayan_project). And in subdirectory my directory structure looks like this:

- Inside the my-vue-project folder, I put Vue.js app.
- In the laravel-app folder, I put your Laravel project.
- The python-app folder is for Python stuff.
- There's also a file named app.py for your Flask app.
- The default.conf file helps Nginx (a web server) work correctly.
- The entrypoint.sh script helps start things up.
- index.php is a PHP file for Laravel app.
- Dockerfile is like a recipe for creating your workspace and build the project.
- docker-compose.yml is a set of instructions for Docker.



### Node:
    -WORKDIR /app
    -COPY package*.json ./
    -RUN npm install
    these commands in the Dockerfile are responsible for preparing the Node.js environment within the Docker container. They set the working directory, copy the project's package configuration files, and install the required Node.js dependencies using npm install. 
    This ensures that when you run your Node.js application inside the container, it has all the necessary dependencies available to it.

### Python:
    -COPY app.py /app/app.py
    -COPY templates /app/templates
    -RUN pip install flask
    These commands copy app.py and templates and install flask applications into /app container.


### Vue:
   -COPY proj-vue /app/proj-vue
   -npm install -g vue-cli
   -vue init webpack proj-vue
   -cd proj-vue
   -npm install
   -npm run dev

### Laravel:
    
   -RUN curl -sS https://getcomposer.org/installer | php -- --install-dir=/usr/local/bin --filename=composer
   -RUN sed -i 's/;clear_env = no/clear_env = no/' /etc/php/7.4/fpm/pool.d/www.conf
   -RUN composer create-project --prefer-dist laravel/laravel /var/www/laravel
   -COPY entrypoint.sh /app/entrypoint.sh
   -RUN chmod +x /app/entrypoint.sh
   -ENTRYPOINT ["/app/entrypoint.sh"]
    these commands in the Dockerfile configure the Laravel environment by installing Composer, adjusting PHP-FPM settings, creating a Laravel project directory, and setting up an entrypoint script to be executed when the container starts.




### Shell-File
    -In script starts services for PHP (version 7.4) and Nginx web server.
    -It runs a Python script, a Node.js application, and sets up a Vue.js development server in the background.
    -Overall, the script helps to set up a combined environment with multiple technologies for development purposes.


### docker-compose.yml

   -Contains configuration of all apps
   -For orchestration


### default.conf

   -listen 100: listen requests that are coming on port 100
   -default.conf defines how Nginx should route requests to different backend services Node.js, Python, Vue.js, handle static files, and process PHP scripts through PHP-FPM. It's a common setup for serving a variety of applications through a single Nginx server.

   - To see your Laravel app, open web browser(firefox) and go to http://172.18.0.5:100/php.
   - For your Vue.js app, go to http://172.18.0.5:100/vue.
   - For your node.js app, go to http://172.18.0.5:100/node.
   - For your python.py app, go to http://172.18.0.5:100/python.


