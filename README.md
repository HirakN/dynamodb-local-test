# Dynamodb-local-test

## Set up local dynaodb
Create containers to setup local dynamodb endpoint
`docker compose up -d`

## Create table
Create table with one key
`aws dynamodb create-table --region eu-west-1 --endpoint http://localhost:8000 --table-name test --attribute-definitions AttributeName=id,AttributeType=S --key-schema AttributeName=id,KeyType=HASH --provisioned-throughput ReadCapacityUnits=2,WriteCapacityUnits=2`

Check table was created
`aws dynamodb list-tables --region eu-west-1 --endpoint-url http://localhost:8000`

## Add entries
Add some items to dynamodb
`aws dynamodb put-item --region eu-west-1 --endpoint-url http://localhost:8000 --table-name test --item '{"id":{"S":"id1"},"name":{"S":"name1"}}'`
`aws dynamodb put-item --region eu-west-1 --endpoint-url http://localhost:8000 --table-name test --item '{"id":{"S":"id3"},"name":{"S":"name1121"}}'`

Check item was added
`aws dynamodb get-item --region eu-west-1 --endpoint-url http://localhost:8000 --table-name test --key '{"id":{"S":"id1"}}'`

Scan the table
`aws dynamodb scan --region eu-west-1 --endpoint-url http://localhost:8000 --table-name test`

## Shutdown
`docker-compose down`

### Persistance
When you want a persistant db, edit the compose yaml file to comment in the relevant lines. Then, make sure to change ownership of the folder created to give the user in the container with id 1000 permissions
`sudo chown 1000:1000 ./docker -R`