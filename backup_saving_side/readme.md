
# Rest server

Rest server to backup data.


## To build the image :

clone this https://github.com/restic/rest-server

`docker build -t restic/rest-server:latest .`



## Init container

Set .env file


Start rest server : 
`docker-compose up -d`


Create a user with password. Something like (replace container id, user and pw):

`docker exec -t  prod_backup_backup_restserver_1 create_user ${REST_SERVER_USER} ${REST_SERVER_PW}`


