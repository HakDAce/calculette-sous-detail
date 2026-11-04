# Calculette sous-détail VRD

Application web pour chiffrer un sous-détail de prix VRD sur téléphone :
déboursé sec par blocs, coefficient de vente, prix de vente, valeur cible et export au format détail QDV.

## Ce que fait l'application

- **Ouvrage** : n° de prix, désignation, unité, rendement journalier, quantité (facultative).
- **Blocs du déboursé sec** : main-d'œuvre (à l'heure ou à la journée), matériel, matériaux (remise / ristourne, transport, pertes, aide épaisseur × densité), évacuation en 3 lignes (camion à la journée, chauffeur à l'heure, décharge à la tonne), sous-traitance.
- **Coefficient** : K direct, ou construit (encadrement, sécurité, magasin, siège, études, bénéfice et aléas) ; coefficient séparé pour la sous-traitance.
- **Prix de vente** arrondi au centime supérieur (option), total, marge.
- **Valeur cible** : tu fixes le prix de vente, l'application calcule le rendement nécessaire et alerte si l'écart est trop fort.
- **Devis** : regroupe des ouvrages avec leurs quantités (et des titres de chapitre) pour obtenir le prix total : total HT, TVA, TTC, déboursé sec, marge et durée estimée. Les prix suivent les sous-détails en direct. Export Excel en 3 onglets (Devis, Analyse interne, Détail QDV).
- **Métré façon QDV** : variables du devis et de chapitre (ex. `S = 4000`, `E = 0,05`) et quantités en formule (`S*E` → 200 m³, `(L+2)*l`, `15%*S`). Virgule décimale, × ÷ acceptés, majuscules/minuscules distinctes (L ≠ l). Le bouton **ƒx** ouvre le clavier lettres.
- **Adapter pour ce chantier** : copie d'un ouvrage propre au devis (modifiable sans toucher l'ouvrage de base ; les prix restent ceux de la bibliothèque).
- **Frais de chantier ventilés** (option par devis) : répartis au prorata du déboursé sec de chaque poste (DS → DSTU), puis K. **K du devis** optionnel. Alerte de double compte si « encadrement » est déjà dans le K des réglages.
- **Ressources du devis** : heures, jours, tonnes et déboursés par ressource. Export Excel en 5 onglets (Devis, Analyse interne, Détail QDV avec titres de chapitre, Ressources, Métré).
- **Bibliothèque** de ressources, sans aucun prix par défaut. **Import Excel** : télécharge le modèle (ta bibliothèque actuelle), saisis les prix, réimporte ; aperçu des changements avant application, rien n'est effacé.
- **Export Excel au format détail QDV** (onglets « Détail QDV » et « Récap »), copie pour Excel, sauvegarde et restauration (.json).

## Où sont les données

Toutes les données (prix, ouvrages, réglages) restent **dans le navigateur du téléphone** (stockage local).
Rien n'est envoyé sur internet, et le dépôt GitHub ne contient **aucun prix**.

Conséquence : si tu vides les données de Safari, supprimes l'icône de l'écran d'accueil ou changes de téléphone, tout est perdu.
Fais régulièrement **Réglages → Télécharger la sauvegarde**.

## Mise en ligne avec GitHub Pages

1. Crée un dépôt sur GitHub (par exemple `calculette-sous-detail`) et envoie-y tous les fichiers de ce dossier.
2. Dans le dépôt : **Settings → Pages → Build and deployment → Source : Deploy from a branch**, branche `main`, dossier `/ (root)`, puis **Save**.
3. Après une à deux minutes, le site est disponible à l'adresse `https://<ton-identifiant>.github.io/calculette-sous-detail/`.

> GitHub Pages est gratuit pour un dépôt **public**. Le code est alors visible, mais pas tes prix, qui restent sur ton téléphone.

## Installation sur iPhone

1. Ouvre l'adresse du site dans **Safari**.
2. Bouton **Partager → Sur l'écran d'accueil**.
3. Lance l'application depuis l'icône : elle s'ouvre en plein écran et fonctionne hors connexion après la première ouverture.

Attention : l'application installée sur l'écran d'accueil et Safari n'ont **pas le même stockage**. Utilise toujours la même (de préférence l'icône).

## Mettre à jour l'application

Remplace `index.html` dans le dépôt, puis change `VERSION` dans `sw.js` (par exemple `sdp-v3`).
Tes données ne sont pas touchées par une mise à jour.

## Fichiers

| Fichier | Rôle |
|---|---|
| `index.html` | toute l'application (interface, calculs, export) |
| `manifest.webmanifest` | nom, couleurs et icônes pour l'écran d'accueil |
| `sw.js` | cache hors connexion |
| `icons/` | icônes de l'application |
| `vendor/` | bibliothèque d'export Excel (SheetJS) et sa licence |
| `.nojekyll` | sert les fichiers tels quels sur GitHub Pages |

## Limites

- Outil d'aide au chiffrage personnel : il ne remplace pas le logiciel de chiffrage officiel de l'entreprise. Vérifie la politique interne avant de l'utiliser pour une offre.
- L'export reprend la structure du détail QDV (lignes Ouv. / Art., formules `[Ratio]`), mais il n'est pas réimportable tel quel dans QDV.
