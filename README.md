# 🏍️ Météo Trajet Moto

Application web d'une seule page qui affiche la météo **point par point le long d'un trajet moto**, avec un score de confort et des alertes pensées pour le deux-roues. On saisit un itinéraire (villes ou fichier GPX), et l'app calcule la météo à l'heure estimée de passage à chaque étape.

Le tout tient dans un seul fichier `index.html`, sans build ni serveur : il suffit de l'ouvrir dans un navigateur ou de l'héberger en statique (GitHub Pages).

## Fonctionnalités

- **Météo le long de la route** : échantillonnage automatique tous les ~35 km entre les villes, avec l'heure de passage estimée d'après la vitesse moyenne (ou la durée réelle calculée pour un GPX).
- **Score de confort moto (0-100)** : combine le ressenti thermique, la pluie, le type de temps et le vent relatif à la route. Un point dangereux (orage, forte pluie) ne peut pas être « noyé » par la moyenne, et un orage sur le parcours plafonne le score.
- **Ressenti thermique (windchill)** : température ressentie à l'allure, calculée avec la formule JAG/TI en tenant compte de la vitesse de roulage. À 90 km/h, 8 °C réels deviennent ~1 °C ressenti.
- **Rafales de vent** : c'est la rafale, plus dangereuse qu'un vent constant, qui pilote la pénalité vent, avec prise en compte de l'angle par rapport à la route (vent de face, de travers, portant).
- **Risque de route mouillée** 💦 : détecte si de la pluie est tombée dans les 3 h précédant le passage — chaussée encore humide donc adhérence réduite.
- **Brouillard** 🌫️ : signalé comme danger de visibilité.
- **Détection d'orage entre deux points** : la route est ré-analysée finement (tous les ~12 km) pour repérer les cellules orageuses étroites qui tomberaient *entre* les points météo affichés et passeraient sinon inaperçues.
- **Deux modes d'entrée** : liste de villes (avec autocomplétion) ou import d'une trace **GPX**.
- **Affichage/masquage des panneaux météo** sur la carte via un interrupteur.
- **Résumé texte du trajet** exportable en `.txt`, avec score, section vigilance et détail par point.
- **Carte interactive** : panneaux météo cliquables, marqueurs de danger, tracé de l'itinéraire.

## Utilisation

1. Ouvrir `index.html` dans un navigateur (ou visiter la page hébergée).
2. Choisir le **jour** et l'**heure de départ**, et régler la **vitesse moyenne**.
3. Saisir les villes de départ, d'étape et d'arrivée — **ou** importer un fichier **GPX**.
4. Cliquer sur **Afficher la météo**.
5. Consulter la carte et la liste ; cliquer sur **Résumé du trajet** pour l'export texte.

## Stack technique

Application 100 % côté client (HTML/CSS/JavaScript), sans dépendance de build.

| Usage | Service |
|---|---|
| Fond de carte | [Leaflet](https://leafletjs.com/) + tuiles OpenStreetMap |
| Prévisions météo | [Open-Meteo](https://open-meteo.com/) |
| Autocomplétion d'adresses (FR) | [Base Adresse Nationale](https://adresse.data.gouv.fr/) |
| Géocodage (repli) | [Nominatim](https://nominatim.org/) (OpenStreetMap) |
| Calcul d'itinéraire routier | [OSRM](https://project-osrm.org/) |

Toutes ces APIs sont publiques et gratuites ; aucune clé n'est nécessaire.

## Hébergement

Étant un fichier statique unique, l'app se déploie tel quel sur **GitHub Pages**, Netlify, Vercel, ou n'importe quel serveur web. Placer `index.html` à la racine du dépôt suffit.

## Confidentialité

Aucun compte, aucun stockage serveur. Les itinéraires saisis servent uniquement à interroger les APIs météo et cartographiques depuis le navigateur.

## Crédits

Développé par [MG](https://github.com/tthma). Données cartographiques © contributeurs OpenStreetMap, météo © Open-Meteo.
