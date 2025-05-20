# DevOps
# TP1 01 - Docker 
1-1 : utiliser -e lors de la création du container, permet de ne pas stocker les variables d'environnement dans l'image, limitant leur accès dans le but de renforcer la sécurité. On peut toujours les modifier sans avoir besoin de reconstruire l'image. 

1-2 : nous avons besoin d'un volume car le container est éphemère donc si je le supprime toutes les données le seront aussi. Le fait de créer un volume afin de stocker les données de notre container. 

1-3 : build une image : docker build -t my-postgres-db .
      création d'un container : docker run \
  --name my-postgres-container \
  --net app-network \
  -d \
  -e POSTGRES_DB=db \
  -e POSTGRES_USER=usr \
  -e POSTGRES_PASSWORD=pwd \
  -v ~/TP1_postgres_data:/var/lib/postgresql/data \
  my-postgres-db

création du container adminer : docker run \
  -p 8090:8080 \
  --net app-network \
  --name adminer \
  -d \
  adminer

1-4: Le but est d'avoir l'image la plius légère possible, pour permettre un démarrage rapide. 

docker run \
  --name backend-api \
  --network app-network \
  -p 8080:8080 \
  -e DB_URL=jdbc:postgresql://postgres:5432/db \
  -e DB_USERNAME=usr \
  -e DB_PASSWORD=pwd \
  my-backend-api


1-5: Un reverse proxy, c'est le fait de faire un intermédiaire entre le client et l'API ici. On en a besoin, pour créer un accès simplifier on passe de : http://localhost:8080/ à http://localhost/. Ça permet également d'unifier les ports, on a plus besoin d'exposer sur plusieurs ports. Et enfin comme le reverse proxy permet d'organiser les différentes connexions. 

1-6 : Le fichier docker-compose est important puisqu'il permet la gestion de plusieurs Docker. En plus, il facilite le démarrage, la dépendance, l'arrêt des différents containers. Permet aussi de gérer les différents networks et volumes associés. 

1-7 : Les commandes les plus importantes sont : docker-compose up --> démarre les services du fichiers
                                                docker - compose down --> arrête et supprimer les containers
                                                docker-compose build --> construction des images qui ont un build spécifié
                                                docker-compose ps --> affiche les conteneurs
                                                docker-compose restart --> relance les containers
                                                docker-compose stop --> arrête et supprime les containers

1-9 : - docker login --> connecte à docker HUB
docker tag tp1_postgres-database marionbln/tp1_postgres-database:1.0 --> tag de l'image
docker push marionbln/tp1_postgres-database:1.0 --> publication de l'image dans mon docker HUB

1-10 : Si je publie les images cela permet : 
- que d'autres développeurs aient accès à mes images, 
- de déployer l'image sur d'autres machine 
- de pouvoir versionner les images 


 

