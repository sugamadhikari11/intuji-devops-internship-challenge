# 🚢🔧 Docker and 🤖 Jenkins CI/CD Pipeline Setup

## 1️⃣: Create a 🐳 DockerHub Account
If you don't already have a DockerHub account, create one. Choose an easy-to-remember username, as it will be required later when logging into Docker through the terminal.

---

## 2️⃣: Clone the Project 📂 Repository
Clone the project from your desired repository.

---

## 3️⃣: Install 🐳 Docker
Install Docker on your computer from DockerHub. For 🐧 Linux (e.g., Ubuntu), you can use the installation script provided on the Docker website.

**📝 Note:**
Be aware of permission issues that may arise. Ensure you grant the necessary 📖 read and ✍️ write permissions to Docker and all related files as you proceed through the steps below.

---

## 4️⃣: Create a Dockerfile 📝
Open the cloned project on your computer. Create a `Dockerfile` (note: no file extension) in the 📁 root directory of the project (the same directory where the `README.md` file is located).

---

## 5️⃣: Write Dockerfile ⚙️ Configuration
Add the following code to your `Dockerfile` to set up your 🛠️ container and manage essential configurations:

```Dockerfile
# 🐘 Use the official PHP-Apache image as the base
FROM php:8.0-apache

# 🔄 Enable mod_rewrite for Apache (useful for PHP projects)
RUN a2enmod rewrite

# 📂 Copy the entire project into the container
COPY . /var/www/html/

# 🛠️ Set permissions for the web server
RUN chown -R www-data:www-data /var/www/html/

# 🔓 Expose port 80 (HTTP)
EXPOSE 80

# 📜 Set the directory index to index.php (or index.html)
RUN echo "DirectoryIndex index.php index.html" >> /etc/apache2/apache2.conf

RUN echo "<Directory /var/www/html/>" >> /etc/apache2/apache2.conf
RUN echo "    AllowOverride All" >> /etc/apache2/apache2.conf
RUN echo "    Require all granted" >> /etc/apache2/apache2.conf
RUN echo "</Directory>" >> /etc/apache2/apache2.conf
RUN echo "ServerName localhost" >> /etc/apache2/apache2.conf

# 🚀 Start the Apache server
CMD ["apache2-foreground"]
```

**📝 Note:** Ensure that `index.php` exists in the `src` directory if you plan to use this configuration.

---

## 6️⃣: Build and Push Docker Image 🐳📤
1. Navigate to the directory containing your `Dockerfile`:
    ```bash
    cd foldername
    ```
2. Build your Docker container:
    ```bash
    docker build -t username/clonedfoldername .
    ```
3. Log in to Docker:
    ```bash
    docker login
    ```
    This command provides a 🔗 link and one-time password for verification.
4. Push your 🛠️ image to DockerHub:
    ```bash
    docker push username/clonedfoldername
    ```

---

## 7️⃣: Create a `docker-compose.yml` File 📋
Create a `docker-compose.yml` file in the 📁 root directory of your project. Add the following code:

```yaml
version: '3.8'

services:
  app:
    image: your-dockerhub-username/php-hello-world
    ports:
      - "8080:80"
    restart: always
```

---

## 8️⃣: Start Docker Container 🏃‍♂️
Run the following command in the terminal to start the container:

```bash
docker-compose up
```

Access the application locally at:

[http://localhost:8080](http://localhost:8080)

If it works, you have successfully created a 🐳 Docker image and pushed it to DockerHub.

---

## 9️⃣: Install 🤖 Jenkins
To install Jenkins:
- On 🐧 Linux, use the installation script provided on the Jenkins website.
- On 🪟 Windows, download and install Jenkins using the installer from the official site.

**📦 Dependencies:** Ensure you install all necessary dependencies. One known dependency is ☕ Java. For others, refer to Jenkins documentation or use tools like ChatGPT to get assistance.

---

## 🔟: Start Jenkins 🚦
1. Start Jenkins:
    - It will run on a default port (8080). Since the application is already set up on port 8080, change the Jenkins port in the configuration file to avoid conflicts (e.g., 81).
2. Access Jenkins:
    ```
    http://localhost:8081
    ```
3. When prompted for a 🔑 password, check your terminal for the password generated during Jenkins setup.

---

## 1️⃣1️⃣: Configure Jenkins ⚙️
1. Install the suggested 🔌 plugins.
2. Set up the admin user and password.
3. Create a new 🛠️ pipeline:
    - Name it as you wish.
    - Choose "Pipeline" as the workflow type and click OK.
4. Configure the pipeline:
    - Use the Git option and provide the 🔗 link to your repository containing the Dockerfile.
    - Install the following plugins for better integration:
        - **Git plugin:** To work with Git repositories.
        - **Pipeline plugin:** To define Jenkins pipelines.
        - **Docker plugin:** To integrate Docker with Jenkins.
        - **Blue Ocean:** For a modern Jenkins UI.
        - **Credentials Binding Plugin:** For securely managing credentials.

---

## 1️⃣2️⃣: Finalize Pipeline ✅
1. Apply and save your configurations.
2. Your basic CI/CD pipeline is ready! 🎉

---

## 🎉 Happy Coding! 👨‍💻👩‍💻

