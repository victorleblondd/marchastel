# Marchastel — proposition de nouveau site pour la commune

Proposition de nouveau site internet pour la commune de Marchastel (Cantal, 15400), sur le modèle du site de
[Saint-Bonnet-de-Condat](https://saint-bonnet-de-condat.fr/), publiée avec GitHub Pages :
https://victorleblondd.github.io/marchastel/

Le site officiel actuel de la commune reste [marchastel15.fr](https://marchastel15.fr). Tant que la mairie n'a pas
adopté la proposition (`proposition: true` dans `_config.yml`), chaque page affiche un bandeau « Proposition de
nouveau site », le site n'est pas référencé par les moteurs de recherche et les mentions légales sont au nom
de l'auteur de la proposition.

GitHub construit le site automatiquement (Jekyll) à chaque modification de la branche `main`.
Aucune installation n'est nécessaire.

## Sources des contenus

- Les avis de la mairie (textes publiés d'avril à octobre 2026) et le site actuel de la commune (marchastel15.fr) : horaires, séances du conseil municipal, présentation et patrimoine, associations, tri des déchets, fibre optique.
- Le Répertoire national des élus (version du 11 août 2026) : le conseil municipal élu le 15 mars 2026 ; la base nationale des intercommunalités (Banatic) : les groupements dont la commune est membre.
- L'Insee (population légale 2023, répertoire Sirene pour les associations), l'annuaire de l'éducation (école de Lugarde) et Wikipédia (géographie, Léon Boyer).
- Les bases Mérimée et Palissy du ministère de la Culture : l'église Sainte-Croix-et-Saint-Pierre, ses retables et le viaduc de Barajol.
- L'office de tourisme Destination Haut Cantal (restaurant, Gentiane Express), le Parc naturel régional des Volcans d'Auvergne (boucle VTT des Forêts), Gîtes de France et les sites des hébergements.
- Santé.fr (pharmacie) et VigiEau (sécheresse, consulté le 15 octobre 2026).

## Ajouter un avis « Infos & Alertes »

1. Ouvrir `_data/infos_alertes.yml` et copier le modèle (en tête du fichier) **tout en haut de la liste** :
   date, type (`alerte` ou `info`), thème, titre, résumé, et le texte de l'avis.
2. Si l'avis est une affiche : déposer le PDF dans le dossier `documents/infos-alertes/`, nommé
   `AAAA-MM-JJ-sujet-court.pdf` (sans accents ni espaces), et indiquer son nom dans le champ `pdf`.

L'avis apparaît alors sur la page Infos & Alertes et sur l'accueil.
Une alerte récente s'affiche aussi en bandeau rouge sur l'accueil pendant 3 jours
(ou jusqu'à la date indiquée dans `bandeau_jusquau`).

**Affiche disponible en ligne (image ou PDF) :** au lieu de déposer le fichier, ajouter une ligne
`adresse  documents/infos-alertes/AAAA-MM-JJ-sujet.pdf` dans `outils/fichiers-a-recuperer.txt`.
GitHub télécharge le fichier, convertit une image en PDF A4 et l'ajoute au site
(`.github/workflows/recuperer-fichiers.yml`). Plusieurs images séparées par `|` donnent un PDF de plusieurs pages.

## Ajouter une séance du conseil municipal

Ouvrir `_data/elus.yml` et ajouter la séance **en tête de la liste `seances`** : date, date affichée et points de
l'ordre du jour. Elle apparaît sur la page Conseil municipal (`/conseil-municipal/#seances`).

## Ajouter un rendez-vous à l'agenda

Ouvrir `_data/agenda.yml` et ajouter le rendez-vous à sa place, dans l'ordre chronologique : date, date de fin
(facultative), date affichée, titre, détail et lieu (facultatifs). Tant que la liste est vide (`[]`), remplacer
cette ligne par le rendez-vous. Les six prochains rendez-vous s'affichent sur l'accueil (la rubrique n'apparaît
que s'il y en a), tous sur la page Vie locale ; un rendez-vous passé disparaît tout seul le lendemain.

## Ajouter un document à l'affichage légal

1. Déposer le PDF dans le dossier `documents/affichage-legal/`, nommé `AAAA-MM-JJ-sujet-court.pdf`
   (ou ajouter son adresse dans `outils/fichiers-a-recuperer.txt`).
2. Ouvrir `_data/affichage_legal.yml` et copier le modèle **en tête de la liste `documents`** :
   date de publication, type (`compte-rendu`, `deliberation`, `proces-verbal`, `convocation`,
   `arrete-municipal`, `arrete-prefectoral` ou `divers`), numéro (facultatif), titre, nom du PDF.

Les filtres par type et par année apparaissent dès le premier document. Les années proposées se règlent
dans le même fichier (`annees`) ; le filtre « Année » n'apparaît qu'à partir de deux années.

## Publier une version (Release)

Pour marquer une version importante, ajouter un fichier `outils/versions/vX.Y.Z.md`
(par exemple `v1.0.0.md`) : titre, commit marqué, puis les notes.
GitHub crée alors la Release correspondante (`.github/workflows/publier-version.yml`).

## Modifier les informations

| À modifier | Fichier |
|---|---|
| Adresse, téléphone, courriel, horaires de la mairie, page Facebook | `_data/mairie.yml` |
| Maire, adjoints, conseillers, séances du conseil | `_data/elus.yml` |
| Rendez-vous | `_data/agenda.yml` |
| Menu principal | `_data/navigation.yml` |
| Bandeau d'annonce temporaire de l'accueil (texte, dernier jour d'affichage) | `_data/annonce.yml` |
| Encadrés « Sécheresse » (afficher ou masquer, niveau, arrêté) | `_data/secheresse.yml` |
| Pages | `mairie.html`, `vie-pratique.html`, `vie-locale.html`, `decouvrir.html`… |
| Apparence | `assets/css/site.css` (augmenter le numéro `?v=` dans `_includes/head.html` à chaque changement) |
| Proposition / site adopté par la commune | `_config.yml` (`proposition`, `site_officiel_actuel`) |

## Le jour où la mairie adopte le site

1. Dans `_config.yml`, passer `proposition` à `false` (le bandeau disparaît, le site devient référençable
   et les mentions légales passent au nom de la commune).
2. Avec un nom de domaine (par exemple marchastel.fr, au nom de la mairie) : ajouter un fichier `CNAME`
   contenant le domaine, mettre `url` sur `https://le-domaine.fr` et `baseurl` sur `""`, puis configurer
   la zone DNS (comme pour Saint-Bonnet-de-Condat).

## Organisation

- `_layouts/` : gabarits communs des pages
- `_includes/` : éléments réutilisés (avis, agenda, horaires, icônes, dates en français)
- `assets/images/` : photo de l'église et blason du Cantal
- `documents/infos-alertes/` : avis en PDF
- `documents/affichage-legal/` : documents de l'affichage légal en PDF

## Crédits

- Photographie de l'église de Marchastel : Père Igor, [Wikimedia Commons](https://commons.wikimedia.org/wiki/File:Marchastel_%C3%A9glise.jpg), licence CC BY-SA 4.0, image recadrée et réduite.
- Blason du Cantal : dessin de Gretaz et contributeurs (Wikimedia Commons), licence CC BY-SA 3.0, image adaptée.
