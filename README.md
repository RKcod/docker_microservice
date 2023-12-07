# Objectif du Tp : faire communiquer deux applications qui existent dans des differents reseaux à travers un reseau gateway
### Création des reséaux ynov-frontend-network et ynov-backend-network
  ##### docker network create --subnet=10.0.0.0/24 ynov-frontend-network
  ##### docker network create --subnet=10.0.1.0/24 ynov-backend-network
### creation du container gateway
  ##### docker run -d --name --privileged gateway 
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
 
