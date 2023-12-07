# Objectif du Tp : faire communiquer deux applications qui existent dans des differents reseaux à travers un reseau gateway
### Création des reséaux ynov-frontend-network et ynov-backend-network
  ##### docker network create --subnet=10.0.0.0/24 ynov-frontend-network
  ##### docker network create --subnet=10.0.1.0/24 ynov-backend-network
### creation du container gateway
  ##### docker run -d --name --privileged gateway nginx
l'option privileged ici nous permet d'avoir tous les droits sur le container afin de pouvoir configurer notre table de routage 
### connection des networks au gateway 
  ##### docker network connect ynov-frontend-network gateway 
  ##### docker network connect ynov-backend-network gateway 
### configuration de la table de routage 
  #### docker exec gateway ip route add 10.0.0.0/24 via 10.0.0.2
  #### docker exec gateway ip route add 10.0.1.0/24 via 10.0.1.2
### Connection en bash sur le gateway pour vérifier la table de routage
  #### docker exec -it gateway bash 
  #### ip route show

### Création des containers dans les réseaux ynov_frontend-network et ynov_frontend-network
#### docker run -d --name prestashop-ynov --network=ynov-frontend-network -e PS_DEV_MODE=false -e PS_INSTALL_AUTO=0 -p 8001:80 -d prestashop/prestashop:1.7-7.0
#### docker run -d  --name mariadb --network=ynov-backend-network --env MARIADB_ROOT_PASSWORD=kenya_ronaldo  mariadb:latest

### Inspection des network pour se rassurer que les container ont été ajoutés
  #### docker network inspect ynov-frontend-network
  #### docker network inspect ynov-backend-network
une fois cela fait on 'a la possibilité de voir les adresses ip des containers et on peut se connecter sur le containers prestashop-ynov pour pinguer mariadb sans soucis.
  
