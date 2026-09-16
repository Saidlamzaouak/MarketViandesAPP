# MarketViandes — maquette de l'application client

Prototype cliquable de l'application de commande de viande et volaille destinée aux
clients de MarketViandes. Bilingue **français / darija marocaine (RTL)** — bouton de langue en haut de l'écran.
Tous les produits se vendent **au kilo**.

> Maquette de travail, non contractuelle. Données, prix et stocks fictifs.
> Back-office cible : Odoo 16.

## Voir la maquette

Une fois publiée (voir ci-dessous) :

```
https://<votre-compte>.github.io/marketviandes-maquette/
```

## Contenu

| Fichier | Rôle |
|---|---|
| `index.html` | La maquette complète — un seul fichier, aucune dépendance à installer |
| `.nojekyll` | Évite le traitement Jekyll par GitHub Pages |
| `README.md` | Ce document |

L'application ne nécessite ni serveur, ni base de données, ni build.
Un double-clic sur `index.html` suffit pour l'ouvrir en local.

## Publier sur GitHub Pages

1. Créer un dépôt sur GitHub, par exemple `marketviandes-maquette`.
   Le dépôt doit être **public** pour que GitHub Pages fonctionne sur un compte gratuit.
2. Déposer `index.html`, `.nojekyll` et `README.md` à la racine
   (bouton *Add file → Upload files*, puis *Commit changes*).
3. Ouvrir **Settings → Pages**.
4. Dans *Build and deployment* : source **Deploy from a branch**,
   branche **main**, dossier **/ (root)**, puis *Save*.
5. Attendre une à deux minutes. L'adresse publique s'affiche en haut de la page Pages.

C'est cette adresse à envoyer au client.

### En ligne de commande

```bash
git init
git add .
git commit -m "Maquette application client MarketViandes"
git branch -M main
git remote add origin https://github.com/<votre-compte>/marketviandes-maquette.git
git push -u origin main
```

Puis activer Pages comme aux étapes 3 à 5.

## Autres façons de la publier

| Solution | Quand la choisir |
|---|---|
| **GitHub Pages** | Partage rapide, gratuit, adresse stable |
| **Serveur MarketViandes** | Le plus propre pour un client : déposer `index.html` dans un dossier servi par nginx, par exemple `demo.marketviandes.com` |
| **Netlify Drop** | Glisser-déposer le dossier sur `app.netlify.com/drop`, lien immédiat, sans compte Git |

### Exemple de bloc nginx

```nginx
server {
    listen 80;
    server_name demo.marketviandes.com;
    root /var/www/marketviandes-maquette;
    index index.html;
}
```

Penser à ajouter le certificat TLS (Certbot) avant de communiquer l'adresse.

## Ce que la maquette démontre

- **Disponibilité du jour** : le client ne voit que ce qui a été publié le matin,
  avec l'heure de mise à jour et l'heure limite de commande.
- **Vente au kilo uniquement** : le client saisit un nombre de kilos, avec des raccourcis
  5 / 10 / 20 kg. Le calibre moyen d'une pièce reste affiché à titre indicatif.
- **Facturation au poids pesé** : le montant du panier est estimatif, le montant définitif
  est calculé après pesée à l'atelier. Le bouton *Simuler la pesée* de l'écran de suivi
  sert à montrer ce basculement en réunion.
- **Créneaux réels** : seuls les jours de tournée de la zone du client sont proposés.
- **Encours et factures** : plafond autorisé, montant échu.
- **Re-commande** en un geste depuis une commande passée.

## Personnaliser

Tout est dans `index.html` :

| À modifier | Où chercher dans le fichier |
|---|---|
| Couleurs de la marque | Bloc `:root{ … }` en haut du CSS, variables `--accent`, `--ink`, `--line` |
| Textes français et darija | Objet `DICT` au début du script |
| Produits, prix, stocks (en kg) | Tableau `PRODUCTS` |
| Raccourcis de quantité | Constante `QUICK_KG` |
| Créneaux de livraison | Tableau `SLOTS` |
| Minimum de commande | Constante `MIN_ORDER` |

Les pictogrammes de produits sont provisoires : ils doivent être remplacés par des
photos réelles avant toute présentation commerciale large.

## Licence

Document de travail réalisé par Lamzaouak Innovation pour MarketViandes.
Usage interne au projet.
