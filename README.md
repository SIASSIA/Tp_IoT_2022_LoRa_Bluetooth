Ce projet vise à établir une communication bidirectionnelle entre deux appareils utilisant la technologie LoRa (Long Range). 

###Partie Émetteur####

Dans ce scénario, mon dispositif agit en tant qu'émetteur. L'objectif principal est de configurer une liaison LoRa avec le récepteur. Pour ce faire, nous commençons par acquérir les paramètres de configuration du réseau LoRa via MQTT. Ces paramètres incluent la fréquence, le facteur d'étalement (SF, Spreading Factor) et la bande passante du signal (SB, Signal Bandwidth). 

##Fonctionnement####
Le dispositif commence par se connecter au réseau Wi-Fi spécifié et s'abonne à un broker MQTT public pour recevoir les paramètres de configuration LoRa. Une fois ces paramètres reçus (fréquence, SF, et SB), le dispositif configure le réseau LoRa et commence à envoyer des données. Les données envoyées sont d1 et d2, où d2 représente la valeur RSSI, un indicateur de la puissance du signal reçu.


###Partie récepteur###
Dans ce scénario, notre dispositif agit en tant que récepteur. L'objectif principal est d'établir une liaison LoRa avec un émetteur distant. Voici un guide détaillé sur la configuration, les dépendances et le fonctionnement du code.

##Fonctionnement####

On se connecte d'abord au réseau Wi-Fi spécifié puis à un broker MQTT public pour envoyer les paramètres de configuration au dispositif qui sera chargé de l’émission. Ces paramètres incluent la fréquence, le facteur d'étalement (SF), et la bande passante du signal (SB). 
Une fois la connexion Lora établie on peut enfin recevoir les données venant de l’émetteur, représentées par d1 et d2 qui sont ensuite affichées sur le moniteur série. 




##Configuration et Dépendances ( Emetteur et Récepteur)#####

Le bon fonctionnement du code repose sur l'installation des bibliothèques suivantes dans l’environnement de développement Arduino IDE:
WiFi.h pour la connexion au réseau Wi-Fi.
PubSubClient.h pour la communication MQTT.
ArduinoJson.h pour le parsing des données CSV
On définit ensuite les constantes suivantes dans le fichier de configuration:
`ssid` et `password` pour la connexion au réseau Wi-Fi.
`mqtt_broker`, `topic`, `mqtt_username`, `mqtt_password`, et `mqtt_port` pour la configuration MQTT.

##Points Clés du Code (Emetteur et Récepteur)#####

La fonction `parseCSV` est utilisée pour analyser les paramètres de configuration LoRa reçus via MQTT sous forme de chaîne CSV.
Dans la fonction `setup`, le dispositif établit la connexion Wi-Fi, se connecte au broker MQTT, et configure la communication LoRa avec les paramètres reçus.
La fonction `callback` est déclenchée lors de la réception d'un message MQTT, traitant les données reçues pour configurer le réseau LoRa.
///

Au niveau de l'émetteur, la boucle principale (loop) envoie périodiquement les données d1 et d2 via LoRa et affiche les informations pertinentes sur le moniteur série.
Tandisqu'au nieau du récepteur,la boucle principale (loop) du dispositif traite périodiquement les données reçues et les affiche sur le moniteur série.




En résumé, ce projet illustre comment configurer et utiliser une communication LoRa dans un contexte IoT, en utilisant MQTT pour la transmission des paramètres de configuration. Cela démontre la flexibilité et l'efficacité de LoRa pour la communication à longue distance dans diverses applications IoT.


