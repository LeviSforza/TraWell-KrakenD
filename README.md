
# TraWell-KrakenD

Repository containing KrakenD configuration for TraWell project

## Device vs how to run keycloak

- On Windows use the command: 
 
        docker-compose up 
- If you are using Apple iOS Macbook device simple docker-compose up is not enough. You should do following steps:

1. Clone Keycloak containers repository: 
        
        git clone git@github.com:keycloak/keycloak-containers.git
2. Open server directory 

        cd keycloak-containers/server
3. Checkout at desired versio 

        git checkout 16.1.1
4. Build docker image 

        docker build -t jboss/keycloak:13.0.1 .
5. Run Keycloak 

        docker-compose up


KEYCLOAK_USER and KEYCLOAK_PASSWORD are needed only for the first time running the container. After that these two lines should be commented in docker-compose.yml as otherwise they can lead to unnecessary errors.


##Useful links:

Login in browser:
- Admin console: GET http://localhost:8403/auth/
- Login to users accounts: GET http://localhost:8403/auth/realms/TraWell/account/#/

Other links:
- User info (you need to have access token to get it): GET http://localhost:8403/auth/realms/TraWell/protocol/openid-connect/userinfo
- Keycloak well-known info: GET http://localhost:8403/auth/realms/TraWell/.well-known/openid-configuration
- Health check (to check if KrakenD is working): GET http://localhost:9000/__health
- Health check but protected by keycloak auth (can be used to test if user was correctly authenticated): GET http://localhost:9000/keycloak-protected

How to add role to a user:
- you need to be logged in as user with admin_cli role. You can do it by basic curl for test purposes: 
        
        curl -d "client_id=admin-cli" -d "username=admin@admin"  -d "password=password"  -d "grant_type=password"  "http://localhost:8403/auth/realms/TraWell/protocol/openid-connect/token"

- get all users and find id of a user you need: GET http://localhost:8403/auth/admin/realms/TraWell/users
- get all roles and find id and name of the role that you need: GET http://localhost:8403/auth/admin/realms/TraWell/roles
- assign role to user: POST http://localhost:8403/auth/admin/realms/TraWell/users/{user_id}/role-mappings/realm
  Body:
        [
         {
                "id": role_id,
                "name": role_name,
         }
        ]
- check if role was correctly assigned: GET http://localhost:8403/auth/admin/realms/TraWell/users/{user_id}/role-mappings/realm
