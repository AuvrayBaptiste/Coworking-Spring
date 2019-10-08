# Coworking_Bars #

## Elastic Search 7.2.1 ##

Modifier le fichier de configuration elasticsearch.yml:\
&nbsp;&nbsp;cluster.name: coworking-cluster\
&nbsp;&nbsp;node.name: coworking-node\
&nbsp;&nbsp;path.data: [chemin où stocker les données]\
&nbsp;&nbsp;path.logs: [chemin où stocker les fichiers de log]\
&nbsp;&nbsp;path.repo: [chemin où stocker les sauvegardes]

Relancer Elastic Search pour prendre en compte les modifications.

Vérifier la connexion à la base:\
`curl -X GET 'localhost:9200'`

Créer un index "bars" dans la base:\
`curl -X PUT "localhost:9200/bars"`

Créer les définitions de types pour l'index "bars":\
`curl -X PUT "localhost:9200/bars/_mapping" -H 'Content-Type: application/json' -d '
{
    "properties": {
        "Nom": {
          "type": "text"
        },
        "Adresse": {
          "type": "text"
        },
        "Position": {
          "type": "geo_point"
        },
        "HoraireOuverture": {
          "type":   "date",
          "format": "HH:mm:ss"
        },
        "HoraireFermeture": {
          "type":   "date",
          "format": "HH:mm:ss"
        },
        "TarifParHeure": {
          "type": "float"
        }
    }
}'`

Insérer un bar:\
`curl -X POST 'localhost:9200/bars/_doc/[IdLieu]' -H 'Content-Type: application/json' -d
'{
    "Nom" : "",
    "Adresse" : "",
    "Position" : "[latitude],[longitude]",
    "HoraireOuverture" : "[heures:minutes:secondes]",
    "HoraireFermeture" : "[heures:minutes:secondes]",
    "TarifParHeure" : ""
}'`

Créer un index "reservations" dans la base:\
`curl -X PUT "localhost:9200/reservations"`

Créer les définitions de types pour l'index "reservations":\
`curl -X PUT "localhost:9200/reservations/_mapping" -H 'Content-Type: application/json' -d '
{
    "properties": {
        "NomLieu": {
          "type": "text"
        },
        "NomUtilisateur": {
          "type": "text"
        },
        "EntrepriseUtilisateur": {
          "type": "text"
        },
        "TarifLieu": {
          "type": "float"
        }
    }
}'`

Insérer une réservation:\
`curl -X POST 'localhost:9200/reservations/_doc/[IdReservation]' -H 'Content-Type: application/json' -d
'{
    "NomLieu" : "",
    "TarifLieu" : "",
    "NomUtilisateur" : "",
    "EntrepriseUtilisateur" : ""
}'`

Créer un index "utilisateurs" dans la base:\
`curl -X PUT "localhost:9200/utilisateurs"`

Créer les définitions de types pour l'index "utilisateurs":\
`curl -X PUT "localhost:9200/utilisateurs/_mapping" -H 'Content-Type: application/json' -d '
{
    "properties": {
        "Position": {
          "type": "geo_point"
        },
        "Nom": {
          "type": "text"
        },
        "Entreprise": {
          "type": "text"
        }
    }
}'`

Insérer un utilisateur:\
`curl -X POST 'localhost:9200/utilisateurs/_doc/[IdUtilisateur]' -H 'Content-Type: application/json' -d
'{
    "Position" : "[latitude],[longitude]",
    "Nom" : "",
    "Entreprise" : ""
}'`

Pour supprimer un document:\
`curl -X DELETE "localhost:9200/[index]/_doc/[id]"`

Pour supprimer un index:\
`curl -X DELETE "localhost:9200/[index]"`

Pour effectuer une recherche avec des paramètres:\
`curl -X GET "localhost:9200/[index]/_search?q=[clé]:[valeur]"`

## API Node ##

Installer les modules:\
`npm install [-g pour installation globale] [elasticsearch cors]`

Lancer le serveur:\
`node ./index.js`

