# suivi-delivery-helm

Le **dépôt Helm** de « Suivi de la delivery » : les charts publiés, à installer avec
`helm repo add`, comme ceux de Traefik ou Headlamp.

```bash
helm repo add suivi-delivery https://florent-coulon-deville.github.io/suivi-delivery-helm
helm repo update
helm search repo suivi-delivery
helm install <installation> suivi-delivery/<chart> --version X.Y.Z
```

Les mêmes charts sont aussi dans ghcr.io, en OCI et privés :
`oci://ghcr.io/florent-coulon-deville/charts/<chart>` (après `helm registry login ghcr.io`).

## Comment il est rempli

- La branche **`gh-pages`**, servie par GitHub Pages, porte `index.yaml` et les archives
  `<chart>/<chart>-X.Y.Z.tgz`.
- Elle est écrite **par la CI seulement** : brique `helm-repo.yml` de `suivi-delivery-ci`, à la
  sortie de chaque version (étiquette `vX.Y.Z`), avec le jeton de la GitHub App
  « suivi-delivery-release ».
- Une version publiée ne change jamais : la brique refuse un numéro déjà présent dans l'index.
- **Ne rien modifier à la main sur `gh-pages`.** La branche `main` ne porte que ce README.

## Ce qui est public

Ce dépôt est public, donc les charts aussi (templates et valeurs par défaut). Les images restent
privées dans ghcr.io : le cluster les télécharge avec son Secret de registre. Aucun secret ni
adresse interne dans un `values.yaml` publié.

## Licence

[Apache 2.0](LICENSE) avec la condition **Commons Clause** : chacun peut utiliser, modifier et
redistribuer ce logiciel, y compris en entreprise, mais **pas le vendre**, ni vendre un produit ou
un service (hébergement, conseil, support…) dont la valeur vient, en tout ou en grande partie, de
ce logiciel. Ce n'est donc pas une licence open source au sens de l'OSI. Texte complet :
[LICENSE](LICENSE).

Les charts publiés avant l'ajout de cette condition restent sous Apache 2.0 seule ; elle s'applique aux
versions suivantes, qui embarquent leur fichier `LICENSE`.
