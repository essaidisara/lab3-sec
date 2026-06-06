# lab3-sec

# Mini-rapport d'audit réseau Android avec Burp Suite

## 1. Périmètre

Environnement de test :

* Android Emulator : Pixel 3 API 30
* Outil d'analyse : Burp Suite Community Edition
* Cible : site de démonstration autorisé (example.com)
* Environnement : laboratoire isolé

---

## 2. Configuration

### Proxy Burp

* Listener actif : Oui
* Adresse : 127.0.0.1
* Port : 8080

### Configuration Android

* Proxy : Manual
* Proxy hostname : 10.0.2.2
* Proxy port : 8080



## 3. Preuves collectées

### Preuve 1 : Capture du trafic

Des requêtes HTTP et HTTPS ont été observées dans l'onglet HTTP History de Burp Suite.

Exemples :

* GET http://example.com/
* GET https://www.google.com/complete/search
* GET http://connectivitycheck.gstatic.com/generate_204

### Preuve 2 : Analyse d'une requête

Requête observée :

GET / HTTP/1.1

Host: example.com

Headers identifiés :

* Host
* User-Agent
* Accept
* Accept-Encoding
* Accept-Language
* Connection

Informations observées :

* Méthode : GET
* URL : http://example.com/
* Paramètres : aucun
* Cookies : aucun

### Réponse du serveur

HTTP/1.1 304 Not Modified

Cette réponse indique que la ressource demandée est déjà présente dans le cache du navigateur.

---

## 4. Interception contrôlée

L'interception a été activée temporairement dans l'onglet Intercept.

Résultat :

* La requête a été arrêtée avant transmission.
* Les en-têtes HTTP ont pu être examinés.
* Le bouton Forward a permis de reprendre le trafic.

L'interception a ensuite été désactivée conformément aux consignes du laboratoire.

---

## 5. HTTPS et certificat CA

HTTPS protège les communications entre le client et le serveur grâce au chiffrement.

Par défaut, un proxy ne peut pas lire le contenu HTTPS.

Dans un environnement de laboratoire, un certificat d'autorité de certification (CA) peut être installé temporairement sur l'émulateur afin d'autoriser l'analyse du trafic HTTPS.

Ce certificat doit être supprimé à la fin du laboratoire.

---

## 6. Analyse des risques

Éléments observés :

* Présence d'en-têtes HTTP standards.
* Transmission d'informations d'identification du navigateur (User-Agent).
* Présence possible de cookies sur certaines requêtes HTTPS.

Risques potentiels :

* Exposition d'informations dans les URL.
* Mauvaise gestion des cookies de session.
* Divulgation excessive d'informations dans les en-têtes.

---

## 7. Recommandations défensives

* Limiter les données transmises au strict nécessaire.
* Éviter le stockage d'informations sensibles dans les URL.
* Sécuriser les cookies côté serveur (Secure, HttpOnly, SameSite).
* Utiliser HTTPS pour les communications sensibles.
* Retirer tout certificat de laboratoire après les tests.
* Désactiver le proxy de test à la fin de la séance.

---

## 8. Conclusion

Le trafic réseau de l'émulateur Android a été correctement redirigé vers Burp Suite.

Les objectifs du laboratoire ont été atteints :

* Vérification du passage du trafic via Burp.
* Identification des composants d'une requête HTTP.
* Compréhension du fonctionnement de l'interception.
* Compréhension du rôle d'un certificat CA dans l'analyse HTTPS.
* Production d'une trace d'audit simple et reproductible.

# captures_preuves

<img width="958" height="426" alt="image" src="https://github.com/user-attachments/assets/b943a3da-e44a-4c2a-a7fd-ee3779c2affa" />
<img width="958" height="509" alt="image" src="https://github.com/user-attachments/assets/8fc974f7-a7fd-4f28-92d4-b8efcf50fe6a" />
<img width="278" height="469" alt="image" src="https://github.com/user-attachments/assets/cc871c6b-c412-4c1c-8df6-4c83c0db4c76" />
<img width="955" height="505" alt="image" src="https://github.com/user-attachments/assets/7be7b558-2caf-496c-bca7-e1ad1e060598" />
Requête observée :
GET http://example.com/

Méthode : GET
Hôte : example.com
User-Agent : Android 11 Emulator
Cookies : aucun
Paramètres : aucun
Réponse : HTTP 304 Not Modified
<img width="958" height="271" alt="image" src="https://github.com/user-attachments/assets/daf97fbe-b54d-4014-a67c-0be5169941a9" />
<img width="479" height="495" alt="image" src="https://github.com/user-attachments/assets/4700427b-ce12-4b75-8217-64bf0e6989fd" />
<img width="910" height="458" alt="image" src="https://github.com/user-attachments/assets/52e86d95-7114-4dc3-a09a-86696cdd254c" />
<img width="959" height="503" alt="image" src="https://github.com/user-attachments/assets/348f41cc-1fcd-4241-a4c6-831fe03411ce" />
L'interception active a été réalisée avec Burp Suite.

Une requête HTTPS a été arrêtée avant son envoi au serveur.
Les en-têtes HTTP ont pu être observés, notamment :
- Host
- Cookie
- User-Agent
- Accept-Language

