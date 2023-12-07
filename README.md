# Objectif du Tp : faire communiquer deux applications qui existent dans des differents reseaux à travers un reseau gateway
### Création des reséaux ynov-frontend-network et ynov-backend-network
##### docker network create ynov-frontend-network
##### docker network create ynov-backend-network
### creation du container gateway
##### docker run -d --name --privileged gateway 
l'option privileged ici nous permet d'avoir tous les droits sur le container afin de pouvoir configurer notre table de routage 
### connection des networks au gateway 
##### docker network connect ynov-frontend-network gateway 
##### docker network connect ynov-backend-network gateway 
### confi
