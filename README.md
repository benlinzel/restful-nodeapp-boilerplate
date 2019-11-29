# restful-nodeapp-boilerplate
Boilerplate RESTful Node app with Database and Admin UI  
Stands up a mongodb database, starts a nodejs application which connects to it, and spins up an admin interface for the database with minimal configuration.  

### Stack  
Database: [mongo](https://hub.docker.com/_/mongo)  
Backend: nodejs  
Admin UI: [mongo-express](https://hub.docker.com/_/mongo-express)  

### Dependencies  
Docker  
docker-compose (included with Docker)  

### Setup  
`mkdir db`  
`touch backend/.env`  
Add this content:  
```
MONGO_ROOT_USER=root
MONGO_ROOT_PASSWORD=example
MONGOEXPRESS_LOGIN=dev
MONGOEXPRESS_PASSWORD=dev
```
These values can be whatever you want. First 2 are for mongodb, second 2 are for logging in to mongo-express dashboard.  

### Docker commands
Start:  
`docker-compose up --build`  
> Note: in the first build, the database is created which can require canceling the current start and running it again to get everything to connect  
> Note 2: After building, files should show up in the /db directory which is where the persistent storage volume lives.  

Stop:  
`docker-compose down`  

Recreate DB:  
`docker-compose down`  
`docker volume prune`  
`rm -rf db/*`  
`docker-compose up —build`  

### Database  
Get all posts:  
`curl http://localhost:3000/posts`  

Add new post:  
`curl -i -X POST -H "Content-Type: application/json" -d '{"title":"title","description":"description"}' http://localhost:3000/posts`  

Update post:   
`curl -i -X PUT -H "Content-Type: application/json" -d '{"title":"title2","description":"description2"}' http://localhost:3000/posts/5dd6f023563ca60012f4c622`  

Delete post:  
`curl -X DELETE http://localhost:3000/posts/5dd6f023563ca60012f4c622`  

### URLs  
REST API /Posts: http://localhost:3000/posts  
Database Admin UI: http://0.0.0.0:8081/db/test/posts  
