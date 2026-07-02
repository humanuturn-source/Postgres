
# Video Resource: Learn Postgres in 2 Minutes
## Quick Installation Guide (Docker & pgAdmin)

This companion guide provides the exact steps and commands shown in the video to get your PostgreSQL database and pgAdmin management tool up and running locally using Docker.

---

### Prerequisites
Before running the commands, ensure you have **Docker Desktop** installed and running on your machine:
* [Download Docker Desktop](https://www.docker.com/products/docker-desktop/)

---

### Step 1: Create a Dedicated Docker Network
To allow your PostgreSQL database and pgAdmin containers to communicate securely with each other, create a shared Docker network:

```bash
docker network create pg-network
```

### Step 2: Deploy the PostgreSQL Database Container
Run the following command to pull the official PostgreSQL image and spin up your database container with default administrative credentials:

```bash
docker run --name postgres-db \\
  --network pg-network \\
  -e POSTGRES_USER=admin \\
  -e POSTGRES_PASSWORD=myadmin \\
  -e POSTGRES_DB=dev_db \\
  -p 5432:5432 \\
  -d postgres
```

Database Configuration Reference:
• Container Name: postgres-db
• Network: pg-network
• Username: admin
• Password: myadmin
• Default Database: dev_db
• Local Port: 5432


### Step 3: Deploy the pgAdmin Management Tool Container
To easily view and manage your data through a web interface, deploy the pgAdmin container connected to the same network:

```bash

docker run --name pgadmin-tool \\
  --network pg-network \\
  -e PGADMIN_DEFAULT_EMAIL=sethrajaram100@gmail.com \\
  -e PGADMIN_DEFAULT_PASSWORD=pgadmin \\
  -p 5050:80 \\
  -d dpage/pgadmin4
```

pgAdmin Login Credentials:
• Web Interface URL: http://localhost:5050
• Email / Username: sethrajaram100@gmail.com
• Password: pgadmin


### Step 4: Connecting pgAdmin to Your Postgres Database

1. Open your browser and navigate to http://localhost:5050.
2. Log in using the pgAdmin credentials provided in Step 3.
3. Right-click on Servers -> Register -> Server...
4. Under the General tab, name the connection (e.g., Local Dev DB).
5. Under the Connection tab, use the following configuration:
  
• Host name/address: postgres-db (Note: Since they share a Docker network, you can use the container name as the host) 
• Port: 5432 • Maintenance database: dev_db 
• Username: admin 
• Password: myadmin

6. Click Save, and you are ready to build your database!


---
the host address) • Port: 5432 • Maintenance database: dev_db • Username: admin • Password: myadmin
6. Click Save, and you are ready to build your database!
