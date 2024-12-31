# Setp:1
Create an account in DockerHub, if you dont have any account.
While creating the username give an easy one, since you will need it later while logging in docker through terminal.

# Step:2
Clone the project from the repository.

# Step:3
You can install docker in you computer from docker hub. I had linux ubuntu in my computer, so I just used script.

Note: I guess I don't need  to mention the permission issuse which may arise at any point so be sure to give read and write permssions to docker and all things you will be doing in the below steps.

# Step:4
Open the cloned project in your computer and create the Dockerfile, the docker file does not need any extension.
And it should be in root directory of the project(i.e where your readme is located).

# Step:5
Add this code in you docker file for setting up your container and other behind the scenes things.
NOte: since I said to find the Index.php file in the code below, it will search for it and consider it has index i.e starting point.
SO be sure to create index.php inside your src if you want to use my line of code.

"""
#Use the official PHP-Apache image as the base
FROM php:8.0-apache

#Enable mod_rewrite for Apache (useful for PHP projects)
RUN a2enmod rewrite

#Copy the entire project into the container
COPY . /var/www/html/

#Set permissions for the web server
RUN chown -R www-data:www-data /var/www/html/

#Expose port 80 (HTTP)
EXPOSE 80

#Set the directory index to index.php (or index.html)
RUN echo "DirectoryIndex index.php index.html" >> /etc/apache2/apache2.conf

RUN echo "<Directory /var/www/html/>" >> /etc/apache2/apache2.conf
RUN echo "    AllowOverride All" >> /etc/apache2/apache2.conf
RUN echo "    Require all granted" >> /etc/apache2/apache2.conf
RUN echo "</Directory>" >> /etc/apache2/apache2.conf
RUN echo "ServerName localhost" >> /etc/apache2/apache2.conf

#Start the Apache server
CMD ["apache2-foreground"]
"""


# Step:6
build your docker container using this in terminal:
note: be sure to do cd foldername before using this since it searches for your Dockerfile you created earlier.
" docker build -t username/clonedfoldername ."

Then use " docker login " in terminal
which gives you link and ontime password to verify.
Then use "docker push username/clonedfoldername" to push your image to docker hub.

# Step:7
Then use this code in the newley created docker-composer.yml in root directory of your project.
It connects to your docker iamge and starts the container at port 8080.
'''
version: '3.8'

services:
  app:
    image: your-dockerhub-username/php-hello-world
    ports:
      - "8080:80"
    restart: always
'''
# Step:8
Then use this command in terminal to check if it is working properly.
"docker-compose up"
Access this locally to see if it's working:
http://localhost:8080

If it's working, then you have successfully created a docker image and pushed it to docker hub.

# Setp:9
For installing Install Jenkins. It is very easy in linux: script :)
But if it is windows just install your installer form google .
You can install it in your local machine or in your virtual machine.
It has dependices so be sure to install as well, as for what dependices I forgot, just use chatgpt. I remeber one, it was JAVA.

# Step:10
After installation , You have to start the jenkis.
It will run on certain port , default is 8080. You can change it in config file. Sicne your application is also set up in that same port earlier.
you can change to 81, 82, 83, etc. whatever you want. Anyway I did 81.
http://localhost:8081

You may be asked password,  the password is in your own terminal from where you run it.

# Step:11
After that install the suggested plugins.
Then setup the admin user and password.
After that createnew piplline, name it as you wish.

Then choose common work flow and click ok, then comes the selection part.
There are many but for now to build what i have built just choose the git where you add your newly created git reporsitry link, form where this will access dockerfile you will publish in your repositry.

If you have more energy then please do git workflow as well and other setups, sadly I don't have! GOODNIGHT!
"""
Git plugin: To work with Git repositories.
Pipeline plugin: To define Jenkins pipelines.
Docker plugin: To integrate Docker with Jenkins.
Blue Ocean: For a modern Jenkins UI.
Credentials Binding Plugin: For managing credentials securely.
"""

# Step:12
Then just apply and save, your basic CI-CD pipeline is ready.
Happy Coding!