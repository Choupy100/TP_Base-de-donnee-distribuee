# TP_Base-de-donnee-distribuee1- Démarrer sur site1 un nœud serveur et sur site2 un noeud client.
Site 1
 cd C:\apache-ignite-slim-2.13.0-bin
 cd apache-ignite-slim-2.13.0-bin
 cd bin
 ssh root@207.180.211.231
Site 2
 cd C:\apache-ignite-slim-2.13.0-bin
 cd apache-ignite-slim-2.13.0-bin
 cd bin
 ssh root@149.102.155.141
2-Connectez-vous au site2 depuis votre machine en utilisant l’outils sqlline et exécuter les
requêtes suivantes:
CREATE TABLE City (id LONG PRIMARY KEY, name VARCHAR) WITH
"template=replicated";
INSERT INTO City (id, name) VALUES (1, 'Porto Novo');
INSERT INTO City (id, name) VALUES (2, 'Come');
INSERT INTO City (id, name) VALUES (3, 'Ouidah');
SELECT * FROM City;
Dire ce que vous constatez.
Site 2 Faire:
cd C:\apache-ignite-slim-2.13.0-bin
 cd apache-ignite-slim-2.13.0-bin
 cd bin
 ignite.bat ..\examples\config\example-ignite.xml
 sqlline -u jdbc:ignite:thin://149.102.155.141
 username:--- 
 password: ---
 CREATE TABLE City (id LONG PRIMARY KEY, name VARCHAR) WITH
"template=replicated";
INSERT INTO City (id, name) VALUES (1, 'Porto Novo');
INSERT INTO City (id, name) VALUES (2, 'Come');
INSERT INTO City (id, name) VALUES (3, 'Ouidah');
SELECT * FROM City;

+----+------------+
| ID |    NAME    |
+----+------------+
| 1  | Porto Novo |
| 2  | Come       |
| 3  | Ouidah     |
+----+------------+
Constat: la table city est cree avec les differentes valaurs inserees

3- Stopper le noeud serveur du site1 (CTRL+C) et exécuter la requête depuis l’interface de
sqlline:
SELECT * FROM City;
Dire ce que vous constatez.

a-Aller vers l'interface de creation du noeud serveur(site 1) et faire <<!exit>> puis <<ctrl C>>

b-Au niveau du cmd du site 1 inserrer <<SELECT * FROM City;>>
Constat: il y a Transfert de donnees(replication) du site 2 vers le site 1

4-Depuis l’interface sqlline on exécute les requêtes suivantes:
CREATE TABLE Person (id LONG, name VARCHAR, city_id LONG, PRIMARY KEY (id,
city_id)) WITH "backups=1, affinityKey=city_id";
INSERT INTO Person (id, name, city_id) VALUES (1, 'John Koffi', 3);
INSERT INTO Person (id, name, city_id) VALUES (2, 'Jane GBOBA', 2);
INSERT INTO Person (id, name, city_id) VALUES (3, 'Mary AFFI', 1);
INSERT INTO Person (id, name, city_id) VALUES (4, 'Richard TOGODO', 2);
SELECT * FROM PERSON;

Toujours dans sur la meme interface sqlline executer ces requetes :

CREATE TABLE Person (id LONG, name VARCHAR, city_id LONG, PRIMARY KEY (id,
city_id)) WITH "backups=1, affinityKey=city_id";
INSERT INTO Person (id, name, city_id) VALUES (1, 'John Koffi', 3);
INSERT INTO Person (id, name, city_id) VALUES (2, 'Jane GBOBA', 2);
INSERT INTO Person (id, name, city_id) VALUES (3, 'Mary AFFI', 1);
INSERT INTO Person (id, name, city_id) VALUES (4, 'Richard TOGODO', 2);
SELECT * FROM PERSON;

+----+----------------+---------+
| ID |      NAME      | CITY_ID |
+----+----------------+---------+
| 1  | John Koffi     | 3       |
| 2  | Jane GBOBA     | 2       |
| 3  | Mary AFFI      | 1       |
| 4  | Richard TOGODO | 2       |
+----+----------------+---------+


5- Stopper le noeud client du site2 (CTRL+C) et exécuter la requête depuis l’interface de Depuis l’interface sqlline exécuter les requêtes suivantes:
CREATE TABLE Person (id LONG, name VARCHAR, city_id LONG, PRIMARY KEY (id,
city_id)) WITH "backups=1, affinityKey=city_id";
INSERT INTO Person (id, name, city_id) VALUES (1, 'John Koffi', 3);
INSERT INTO Person (id, name, city_id) VALUES (2, 'Jane GBOBA', 2);
INSERT INTO Person (id, name, city_id) VALUES (3, 'Mary AFFI', 1);
INSERT INTO Person (id, name, city_id) VALUES (4, 'Richard TOGODO', 2);
SELECT * FROM PERSON;

Toujours dans l'interface sqlline executer ces requetes :

CREATE TABLE Person (id LONG, name VARCHAR, city_id LONG, PRIMARY KEY (id,
city_id)) WITH "backups=1, affinityKey=city_id";
INSERT INTO Person (id, name, city_id) VALUES (1, 'John Koffi', 3);
INSERT INTO Person (id, name, city_id) VALUES (2, 'Jane GBOBA', 2);
INSERT INTO Person (id, name, city_id) VALUES (3, 'Mary AFFI', 1);
INSERT INTO Person (id, name, city_id) VALUES (4, 'Richard TOGODO', 2);
SELECT * FROM PERSON;

+----+----------------+---------+
| ID |      NAME      | CITY_ID |
+----+----------------+---------+
| 1  | John Koffi     | 3       |
| 2  | Jane GBOBA     | 2       |
| 3  | Mary AFFI      | 1       |
| 4  | Richard TOGODO | 2       |
+----+----------------+---------+


5- Stopper le noeud client du site2 (CTRL+C) et exécuter la requête depuis l’interface de sqlline:
SELECT * FROM PERSON;
Dire ce que vous constater.
Tirer une conclusion.

a-Aller vers l'interface de creation du noeud serveur(site 2) et faire <<!exit>> puis <<ctrl C>>

b-Au niveau du cmd du site 1 inserrer <<SELECT * FROM PERSON;>>
Constat: La table a ete replique
Conclusion: c'est un systeme de base de donnees distribuees.
# Apache_ignite2
Exercice2 
L'application est pour la gestion des stagires codé en php.
Pré-requis pour l'utiliser avec Ignite :

JDK ;Oracle JDK 8 or 11, Open JDK 8 or 11, IBM JDK 8 or 11

OS :Linux (any flavor), Mac OSX (10.6 and up), Windows (XP and up), Windows Server (2008 and up), Oracle Solaris

ISA : x86, x64, SPARC, PowerPC

Network :No restrictions (10G recommended)

and: PHP Version 7.2 or higher and Composer Dependency Manager. PHP Multibyte String extension. Depending on your PHP configuration, you may need to additionally install/configure it.

Une fois INGITE installez, installez PHP Thin Client en tant que package Composer à l'aide de la commande ci-dessous :
composer require apache/apache-ignite-client.

Pour utiliser le client dans l'application, incluez le fichier vendor/autoload.php, généré par Composer, dans le code source

Avant de vous connecter à Ignite à partir du client Thin PHP, vous devez démarrer au moins un nœud de cluster Ignite.
Sur Windows : 
1 cd {IGNITE_HOME}\bin\
2 ignite.bat ..\examples\config\example-ignite.xml
Ouvrez un autre onglet à partir de votre shell de commande et exécutez à nouveau la même commande.
Décompresser le fichier compressé.
installer le projet dans un répertoire bien connu.
Pius faites les tests 



