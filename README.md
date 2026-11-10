# repday-legal

Pages légales publiques de RepDay : politique de confidentialité, CGU, et la
page web de suppression de compte exigée par Google Play et l'App Store.

**Ce dépôt est public et ne contient que ces pages.** Le code de l'application
reste privé. C'est la seule raison de son existence : GitHub Pages ne publie
pas depuis un dépôt privé sur un plan gratuit, et les trois URLs ci-dessous
doivent être accessibles à n'importe qui — les magasins les vérifient, et la
page de suppression doit rester atteignable par quelqu'un qui n'a plus
l'application installée.

## Publication

Settings → Pages → Source: `Deploy from a branch`, branche `main`, dossier
`/ (root)`. Les URLs deviennent :

| Page | URL |
|---|---|
| Confidentialité | `https://gabrielbdn.github.io/repday-legal/confidentialite.html` |
| CGU | `https://gabrielbdn.github.io/repday-legal/cgu.html` |
| Privacy policy (anglais) | `https://gabrielbdn.github.io/repday-legal/privacy.html` |
| Terms (anglais) | `https://gabrielbdn.github.io/repday-legal/terms.html` |
| Suppression de compte | `https://gabrielbdn.github.io/repday-legal/suppression-compte.html` |

L'origine (`https://gabrielbdn.github.io`) est inchangée par rapport à ce qui
était prévu : `CORS_ORIGINS` côté backend n'a pas à bouger. Seuls les chemins
changent.

## À reporter dans le dépôt applicatif

Ces valeurs sont attendues par le backend et par la build release :

- `ACCOUNT_DELETION_PAGE_URL` → l'URL de suppression ci-dessus ;
- `--dart-define=TERMS_URL` et `--dart-define=PRIVACY_POLICY_URL` → CGU et
  confidentialité.

## Modifier une page

`suppression-compte.html` contient une constante `API_ORIGIN` à renseigner avec
l'origine HTTPS du backend ; tant qu'elle vaut `CHANGE_ME_API_ORIGIN`, la page
s'affiche mais refuse d'appeler l'API — c'est voulu, une page de suppression
qui échoue silencieusement est pire qu'une page désactivée.

Les pages sont du HTML autonome, sans build ni dépendance : les ouvrir dans un
navigateur suffit à les relire avant publication.

## Préparation abonnements — 8 novembre 2026

Les CGU françaises et anglaises locales sont en version 1.3 : elles décrivent
les changements de formule et le transfert d'achat entre comptes RepDay,
validés par Gabriel. Ces modifications n'ont pas été publiées.

Avant publication commerciale : vérifier le parcours de rétractation. Le
téléphone figure dans les mentions légales depuis le 10 novembre 2026. L'entreprise est immatriculée, avec un
début d'activité prévu le **1er décembre 2026**, reconfirmé par Gabriel.
Le suivi technique et les étapes consoles se trouvent dans le dépôt RepDay :
`docs/billing/VALIDATION-2026-11-08.md` et `SUBSCRIPTIONS-SETUP.md`.

## Médiation de la consommation — 10 novembre 2026

Le médiateur de la consommation de RepDay est **CM2C** (Centre de la
Médiation de la Consommation de Conciliateurs de Justice) : convention signée
électroniquement le 10 novembre 2026, échéance le 10 novembre 2029, avec
reconduction tacite selon la convention. La convention, les identifiants et
les reçus restent hors de ce dépôt public.

Coordonnées publiées : 49 rue de Ponthieu, 75008 Paris, France ·
01 89 47 00 14 · litiges@cm2c.net · saisine en ligne sur
`https://www.cm2c.net/declarer-un-litige.php`.

Elles figurent à trois endroits, à modifier ensemble si CM2C change de
coordonnées ou si la convention n'est pas reconduite :

- `cgu.html#mediation` et `terms.html#mediation` (article 14, texte complet
  avec les conditions de recevabilité de l'article L. 612-2) ;
- `mentions-legales.html#mediation` (coordonnées et renvoi à l'article 14) ;
- `cgv.html` renvoie vers `cgu.html#mediation` et `terms.html#mediation`.

## Projet de migration vers repday.fr

Conserver la source HTML ici. Sur le futur hébergeur, servir les fichiers depuis les cinq routes publiques sans authentification. Configurer des réécritures internes (URL sans slash final), ou générer les pages dans le projet web à partir des mêmes fichiers en adaptant les liens relatifs.

| Route repday.fr | Source |
| --- | --- |
| /mentions-legales | mentions-legales.html |
| /cgu | cgu.html |
| /cgv | cgv.html |
| /confidentialite | confidentialite.html |
| /suppression-compte | suppression-compte.html |

Relier les cinq routes au pied de page du site. Vérifier les liens .html et les variantes anglaises sur la cible. Après validation, retirer noindex des nouveaux projets et déclarer leurs URL canoniques. Mettre à jour les liens de build, ACCOUNT_DELETION_PAGE_URL, CORS et les fiches des stores après vérification sur la cible.

Garder toutes les URL GitHub Pages en service pendant la transition. Pour la suppression, conserver le fragment #token lors de tout renvoi, ne jamais le mettre en query et tester aussi un lien émis avant la bascule. Laisser l’ancienne page active tant que les magasins et le flux e-mail n’ont pas été validés avec la nouvelle origine.

Les mentions légales sont complétées depuis le 10 novembre 2026 (éditeur, immatriculation, hébergeurs, médiation). Avant publication, insérer et valider l’encadré réglementaire de garantie adapté à la fourniture continue, vérifier les prix TTC et les offres des stores, la rétractation par magasin, la qualification du contrat et les mécanismes de transfert des données. Coordonner les textes de suppression avec la migration de la file de reprise des médias. La page de rétractation des CGV informe et oriente vers les magasins. L’obligation de fonctionnalité et d’accusé sur support durable reste à valider par contrat et par canal.
