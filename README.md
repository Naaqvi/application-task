Documentation for Application Stack Development Task
Dockerfile:
The Dockerfile consists of four projects: Node, Python, Vue.js, and Laravel. Here is a breakdown of each project's configuration:
Node:
Set the working directory in the container to /app.
Copy package.json and package-lock.json to the working directory.
Run npm install to install Node dependencies.
Python:
Copy the Flask application (app.py) and the templates directory to /app.
Install Flask using pip install flask.
Vue.js:
The Vue.js project was created using the following commands:
Copy

     npm install -g vue-cli
     vue init webpack my-vue-project
     cd my-vue-project
     npm install
     npm run dev
Copy the my-vue-project directory to /app.
Laravel:
Install Composer using curl -sS https://getcomposer.org/installer | php -- --install-dir=/usr/local/bin --filename=composer.
Configure PHP-FPM to clear the environment.
Create a Laravel project in the /var/www/laravel directory using composer create-project --prefer-dist laravel/laravel /var/www/laravel.
The entrypoint of the Dockerfile is defined as follows:
Copy the entrypoint.sh script to /app and make it executable.
Set the entrypoint script to /app/entrypoint.sh.
docker-compose.yml:
The docker-compose.yml file contains the configuration for the following containers:
all-apps container:
Build the container using the Dockerfile in the current directory (.).
Set the container name to mongo.
Restart the container always.
mongo container:
Build the container using the Dockerfile in the ./mongodocker directory.
Set the container name to mongodb.
Restart the container always.
postgreSql container:
Build the container using the Dockerfile in the ./postgreSql directory.
Set the container name to postgreSql.
Restart the container always.
redis container:
Build the container using the Dockerfile in the ./redis directory.
Set the container name to redis.
Restart the container always.
Nginx Server Configurations:
The Nginx server is configured to route requests to different projects as follows:
The Laravel project is running on the default '/' path.
The Python project is running on the '/python' path.
The Node project is running on the '/node' path.
The Vue.js project is running on the '/vue' path.
The Nginx configuration is done using the following template:
Copy

location /<route> {
    proxy_pass http://localhost:8080/;  # Assuming the project runs on port 8080
    proxy_set_header Host $host;
}
Please note that you need to replace <route> with the actual route for each project.
Linked Page URL: http://localhost:8080/;
Page Text: Page Timed Out. Please inform the user that you could not retrieve the page.
