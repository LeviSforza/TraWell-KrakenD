
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


Useful links:
- Admin console: http://localhost:8403/auth/
- Login to users accounts: http://localhost:8403/auth/realms/TraWell/account/#/
- User info (you need to have access token to get it): http://localhost:8403/auth/realms/TraWell/protocol/openid-connect/userinfo
- Keycloak well-known info: http://localhost:8403/auth/realms/TraWell/.well-known/openid-configuration
- Health check (to check if KrakenD is working): http://localhost:9000/__health

