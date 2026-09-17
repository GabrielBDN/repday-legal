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
