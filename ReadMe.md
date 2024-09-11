So far i'm unable to manage to run docker files and docker compose properly lets put it on back burner and use without it.
sudo apt-get update && \
  sudo apt-get install -y dotnet-sdk-8.0

  
create a folder in projects say web

mkdir web in my-projects
cd /my-projects/web

git init

Go to GitHub and create repository for web
Copy the remote URL https://github.com/SaleemAnwarGit/Web.git

cd /my-projects/web
git remote add origin https://github.com/SaleemAnwarGit/Web.git

git add .
git commit -m "Initial commit for web from git"
git push -u origin master


Ensure you have a .gitignore file in both repositories to avoid pushing unnecessary files like node_modules, bin, obj, Docker images, or sensitive data.


.gitignore

# Ignore node_modules
client/node_modules/

# Ignore .NET binaries
server/bin/
server/obj/

# Ignore Docker volumes
/postgres-data/


Create a docker-compose.yml file: Inside the web-dev directory

version: '3.8'
services:
  webapp:
    image: mcr.microsoft.com/dotnet/aspnet:8.0
    build:
      context: ./server
      dockerfile: Dockerfile
    ports:
      - "5000:80"
    depends_on:
      - db
    environment:
      - ASPNETCORE_ENVIRONMENT=Development
      - ConnectionStrings__DefaultConnection=Server=db;Database=mydb;User Id=postgres;Password=postgres;

  db:
    image: postgres:latest
    environment:
      POSTGRES_USER: postgres
      POSTGRES_PASSWORD: postgres
      POSTGRES_DB: mydb
    ports:
      - "5432:5432"
    volumes:
      - postgres-data:/var/lib/postgresql/data

  client:
    image: node:18
    volumes:
      - ./client:/usr/src/app
    working_dir: /usr/src/app
    command: bash -c "yarn install && yarn start"
    ports:
      - "3000:3000"

volumes:
  postgres-data:






docker-compose.yml



Directory for Each Service:

Place your backend (ASP.NET Core) in the server/ directory.
Place your frontend (React) in the client/ directory.
PostgreSQL runs as its own container, and its data will persist in postgres-data.


Build and Run Docker Containers: From the web directory: