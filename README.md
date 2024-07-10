Here's the updated README file for your GitHub repository:

---

# Flask App with MySQL Docker Deploy using Jenkins and Configure SSL Setup

This is a simple Flask app that interacts with a MySQL database. It is deployed on a single server using the CI/CD tool Jenkins. To make it secure, SSL configuration is applied, enabling it to work on HTTPS. The app allows users to submit messages, which are stored in the database and displayed on the frontend.

## Prerequisites
Before you begin, make sure you have the following installed:

- Docker
- Git (optional, for cloning the repository)
- Jenkins
- Nginx

## Setup

1. **Clone this repository (if you haven't already):**
    ```sh
    git clone https://github.com/your-username/your-repo-name.git
    ```

2. **Navigate to the project directory:**
    ```sh
    cd your-repo-name
    ```

3. **Create a `.env` file in the project directory to store your MySQL environment variables:**
    ```sh
    touch .env
    ```

4. **Open the `.env` file and add your MySQL configuration:**
    ```
    MYSQL_HOST=mysql
    MYSQL_USER=your_username
    MYSQL_PASSWORD=your_password
    MYSQL_DB=your_database
    ```

## Usage

1. **Start the containers using Docker Compose:**
    ```sh
    docker-compose up --build
    ```

2. **Access the Flask app in your web browser:**
    - Frontend: http://localhost
    - Backend: http://localhost:5000

3. **Create the `messages` table in your MySQL database:**
    Use a MySQL client or tool (e.g., phpMyAdmin) to execute the following SQL commands:
    ```sql
    CREATE TABLE messages (
        id INT AUTO_INCREMENT PRIMARY KEY,
        message TEXT
    );
    ```

4. **Interact with the app:**
    - Visit http://localhost to see the frontend. You can submit new messages using the form.
    - Visit http://localhost:5000/insert_sql to insert a message directly into the `messages` table via an SQL query.

## Cleaning Up

1. **To stop and remove the Docker containers, press `Ctrl+C` in the terminal where the containers are running, or use the following command:**
    ```sh
    docker-compose down
    ```

## Running the Application Without Docker Compose

1. **First, create a Docker image from the Dockerfile:**
    ```sh
    docker build -t flaskapp .
    ```

2. **Create a network:**
    ```sh
    docker network create twotier
    ```

3. **Attach both containers to the same network so they can communicate:**

    - **MySQL container:**
        ```sh
        docker run -d \
            --name mysql \
            -v mysql-data:/var/lib/mysql \
            --network=twotier \
            -e MYSQL_DATABASE=mydb \
            -e MYSQL_USER=root \
            -e MYSQL_ROOT_PASSWORD=admin \
            -p 3306:3306 \
            mysql:5.7
        ```

    - **Backend container:**
        ```sh
        docker run -d \
            --name flaskapp \
            --network=twotier \
            -e MYSQL_HOST=mysql \
            -e MYSQL_USER=root \
            -e MYSQL_PASSWORD=admin \
            -e MYSQL_DB=mydb \
            -p 5000:5000 \
            flaskapp:latest
        ```

## Jenkins CI/CD Setup

1. **Create a Freestyle project in Jenkins.**
2. **Add the following Execute Shell commands in the Build section:**
    ```sh
    pwd
    cd /var/lib/jenkins/workspace/flask-app-mysql
    sudo apt install docker-compose -y
    sudo docker-compose up -d --build
    sudo docker-compose down
    sudo docker-compose up -d
    ```

## SSL Configuration

1. **Update your system packages:**
    ```sh
    sudo apt update
    ```

2. **Install Certbot and the Certbot Nginx plugin:**
    ```sh
    sudo apt install certbot python3-certbot-nginx
    ```

3. **Run Certbot to obtain and install the SSL certificate:**
    ```sh
    sudo certbot --nginx -d your-domain.com
    ```

Replace `your-domain.com` with your actual domain name.

## Notes

- Make sure to replace placeholders (e.g., `your_username`, `your_password`, `your_database`) with your actual MySQL configuration.
- This is a basic setup for demonstration purposes. In a production environment, follow best practices for security and performance.
- Be cautious when executing SQL queries directly. Validate and sanitize user inputs to prevent vulnerabilities like SQL injection.
- If you encounter issues, check Docker logs and error messages for troubleshooting.

---

I hope you find it useful. If you have any doubt in any of the step then feel free to contact me.
If you find any issue in it then let me know.



<!-- [![Build Status](https://img.icons8.com/color/452/linkedin.png)](https://www.linkedin.com/in/prateek-mudgal-devops) -->


<table>
  <tr>
    <th><a href="https://www.linkedin.com/in/prateek-mudgal-devops" target="_blank"><img src="https://img.icons8.com/color/452/linkedin.png" alt="linkedin" width="30"/><a/></th>
    <th><a href="mailto:mudgalprateek00@gmail.com" target="_blank"><img src="https://img.icons8.com/color/344/gmail-new.png" alt="Mail" width="30"/><a/>
</th>
  </tr>
</table>) 
