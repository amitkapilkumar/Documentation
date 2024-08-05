docker network create employee
docker container run --name mysql --network employee -p 3306:3306 -e MYSQL_ROOT_PASSWORD=root123 -d mysql

docker build --tag=ems-backend:latest .
docker run -p 8080:8080 ems-backend:latest


docker build -t ems-app:1.0 .
docker run -p 3000:3000 --name ems-app -d ems-app:1.0
