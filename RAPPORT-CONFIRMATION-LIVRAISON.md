# Déploiement des fonctionnalités de référence — état réel

> **État historique avant le réexamen en cours :** voir [RAPPORT-PREMIER-COMMIT.md](RAPPORT-PREMIER-COMMIT.md) pour les corrections et le travail restant. Les nombres et résultats ci-dessous décrivent la version auditée précédemment.


## Bilan

**L'application à l'ensemble du dépôt n'est pas terminée et aucune validation réseau réelle n'a été effectuée.** L'inventaire statique compte 133 pages HTML de premier niveau. Au total, **49 dossiers** contiennent un gestionnaire autonome et un module SMS : les deux références, quatre pages d'assurance déjà adaptées, puis 43 pages supplémentaires. Les 28 dossiers listés ci-dessous comportent encore un ou plusieurs formulaires avec téléphone détecté et ne sont pas adaptés. Les autres pages sans téléphone détecté comprennent notamment du contenu, des formulaires de qualification, de consentement, des remerciements et des iframes ; elles nécessitent une revue de parcours, et leur absence dans la liste ne signifie pas qu'elles sont fonctionnelles.

## Comportement installé

- SMS : vérification d'un mobile français, protection contre les réponses de requêtes obsolètes, refus des réponses SMS 200 vides ou non JSON et remise à zéro lorsque le numéro change. Le format effectif des réponses de l’API doit être vérifié en production.
- CRM HelloLead et Google Sheets : envois parallèles ; succès, événement GTM et éventuelle redirection uniquement après une **réponse applicative confirmée**. Un beacon ou fetch `no-cors` ne confirme pas la réception. Le honeypot conserve le comportement silencieux de la référence et n'envoie rien.
- En cas de réponse non confirmée, un lead peut néanmoins être arrivé au CRM. Une nouvelle tentative peut créer un doublon sans déduplication serveur par identifiant. La confirmation CRM CORS ou un relais serveur idempotent doit être validé.
- La source, la catégorie et les données de conversion sont filtrées par consentement. Les réponses textuelles et radio portant le même nom sont conservées toutes les deux. Les destinations de remerciement existantes identifiées sont conservées après confirmation.
- Pour les pages traitées, les anciens scripts SMS concurrents et le simulateur local de succès ont été retirés, sans remplacer les formulaires, les contenus ni les images. Les conteneurs GTM détectés dans les rapports d'origine sont préservés ; le conteneur de référence est utilisé lorsqu'aucun n'était identifié.

## Dossiers équipés — identités CRM à enregistrer ou valider

Les identifiants dérivés des noms de dossiers sont des **propositions de configuration** : leur existence et leur routage dans le CRM ne sont pas prouvés.

| Dossier | formId |
|---|---|
| `LP_reference` | `ADW_LP_VEHICULES_DE_SOCIETE` |
| `acces-internet-et-telephonie-pro` | `ADW_LP_ACCES_INTERNET_ET_TELEPHONIE_PRO` |
| `assurance-agriculteur` | `ADW_LP_ASSURANCE_AGRICULTEUR` |
| `assurance-assurance-professionnelle-iard-cookie` | `ADW_LP_ASSURANCE_ASSURANCE_PROFESSIONNELLE_IARD_COOKIE` |
| `assurance-commerce` | `ADW_LP_ASSURANCE_COMMERCE` |
| `assurance-consultants-societe-conseil` | `ADW_LP_ASSURANCE_CONSULTANTS_SOCIETE_CONSEIL` |
| `assurance-estheticienne-institut-beaute` | `ADW_LP_ASSURANCE_ESTHETICIENNE_INSTITUT_BEAUTE` |
| `assurance-estheticiennes-instituts-beaute-v1` | `ADW_LP_ASSURANCE_ESTHETICIENNES_INSTITUTS_BEAUTE_V1` |
| `assurance-iard-v2` | `ADW_LP_ASSURANCE_IARD_V2` |
| `assurance-marchandise` | `ADW_LP_ASSURANCE_MARCHANDISE` |
| `assurance-multirisques` | `ADW_LP_ASSURANCE_MULTIRISQUES` |
| `assurance-professionnelle-iard` | `ADW_LP_ASSURANCE_PROFESSIONNELLE_IARD` |
| `assurance-professionnelle-tns-v2` | `ADW_LP_ASSURANCE_PROFESSIONNELLE_TNS_V2` |
| `assurance-protection-sociale-collective` | `ADW_LP_ASSURANCE_PROTECTION_SOCIALE_COLLECTIVE` |
| `assurance-rc-pro` | `ADW_LP_ASSURANCE_RC_PRO` |
| `assurance-tns` | `ADW_LP_ASSURANCE_TNS` |
| `assurance-tns-pro-v2-adw` | `ADW_LP_ASSURANCE_TNS_PRO` |
| `automobile` | `ADW_LP_AUTOMOBILE` |
| `celebrez-le-noel-des-salaries-avec-kadeos` | `ADW_LP_CELEBREZ_LE_NOEL_DES_SALARIES_AVEC_KADEOS` |
| `complementaire-retraite-tns-v2` | `ADW_LP_COMPLEMENTAIRE_RETRAITE_TNS_V2` |
| `ecomobility` | `ADW_LP_ECOMOBILITY` |
| `edenred-ticket-restaurant-juillet-v1` | `ADW_LP_EDENRED_TICKET_RESTAURANT_JUILLET_V1` |
| `energie` | `ADW_LP_ENERGIE` |
| `fiat-pro` | `ADW_LP_FIAT_PRO` |
| `geolocalisation` | `ADW_LP_GEOLOCALISATION` |
| `geolocalisation-de-flotte` | `ADW_LP_GEOLOCALISATION_DE_FLOTTE` |
| `mercedes-benz-mercedes-benz-evito` | `ADW_LP_MERCEDES_BENZ_MERCEDES_BENZ_EVITO` |
| `mercedes-benz-nouvel-ecitan-fourgon` | `ADW_LP_MERCEDES_BENZ_NOUVEL_ECITAN_FOURGON` |
| `mercedes-benz-sprinter` | `ADW_LP_MERCEDES_BENZ_SPRINTER` |
| `nissan-ariya` | `ADW_LP_NISSAN_ARIYA` |
| `nissan-juke` | `ADW_LP_NISSAN_JUKE` |
| `panneaux-photovoltaiques-energie-solaire` | `ADW_LP_PANNEAUX_PHOTOVOLTAIQUES_ENERGIE_SOLAIRE` |
| `securite-professionnels` | `ADW_LP_SECURITE_PROFESSIONNELS` |
| `still-manutention` | `ADW_LP_STILL_MANUTENTION` |
| `suivi-de-vehicules` | `ADW_LP_SUIVI_DE_VEHICULES` |
| `ticket-restaurant` | `ADW_LP_TICKET_RESTAURANT` |
| `ticket-restaurant-` | `ADW_LP_TICKET_RESTAURANT_VARIANTE` |
| `ticket-restaurant-septembre` | `ADW_LP_TICKET_RESTAURANT_SEPTEMBRE` |
| `ticket-restaurant-septembre-btp` | `ADW_LP_TICKET_RESTAURANT_SEPTEMBRE_BTP` |
| `tns-prevoyance-v2` | `ADW_LP_TNS_PREVOYANCE_V2` |
| `tns-prevoyance-v2-adw-test` | `ADW_LP_TNS_PREVOYANCE_V2_ADW_TEST` |
| `too-good-to-go` | `ADW_LP_TOO_GOOD_TO_GO` |
| `typ-formulaires-form-typ-vehicules` | `ADW_LP_TYP_FORMULAIRES_FORM_TYP_VEHICULES` |
| `typ-formulaires-typ-caisses-enregistreuse` | `ADW_LP_TYP_FORMULAIRES_TYP_CAISSES_ENREGISTREUSE` |
| `typ-formulaires-typ-energie-form` | `ADW_LP_TYP_FORMULAIRES_TYP_ENERGIE_FORM` |
| `typ-formulaires-typ-panneaux-form` | `ADW_LP_TYP_FORMULAIRES_TYP_PANNEAUX_FORM` |
| `une-rentree-sous-le-signe-du-pouvoir-d-achat` | `ADW_LP_UNE_RENTREE_SOUS_LE_SIGNE_DU_POUVOIR_D_ACHAT` |
| `vehicules-de-societe-hd` | `ADW_LP_VEHICULES_DE_SOCIETE_HD` |
| `vehicules-utilitaires` | `ADW_LP_VEHICULES_UTILITAIRES` |

## Formulaires téléphone non adaptés (détection statique)

- `alfaromeo-tonale` : 1 formulaire(s) détecté(s)
- `assurance-estheticiennes-institut-beaute` : 1 formulaire(s) détecté(s)
- `assurance-test-telephone` : 1 formulaire(s) détecté(s)
- `assurances-professionnelles` : 1 formulaire(s) détecté(s)
- `ayvens-france` : 1 formulaire(s) détecté(s)
- `cartes-carburant` : 1 formulaire(s) détecté(s)
- `dacia-jogger` : 1 formulaire(s) détecté(s)
- `edenred-kadeos` : 1 formulaire(s) détecté(s)
- `formulaire-globale` : 1 formulaire(s) détecté(s)
- `gamme-de-rayonnage-actiflip-hd` : 1 formulaire(s) détecté(s)
- `gamme-de-rayonnage-actiflip-v4` : 1 formulaire(s) détecté(s)
- `intuis` : 1 formulaire(s) détecté(s)
- `lexus-lbx` : 1 formulaire(s) détecté(s)
- `lexus-lbx-2` : 2 formulaire(s) détecté(s)
- `mitsubishi-fuso` : 1 formulaire(s) détecté(s)
- `paritel` : 1 formulaire(s) détecté(s)
- `paritel-vous-rembourse` : 1 formulaire(s) détecté(s)
- `primagaz` : 1 formulaire(s) détecté(s)
- `primagaz-obtenez-votre-gaz-propane-a-prix-fixe` : 1 formulaire(s) détecté(s)
- `rc-pro-consultant-conseil-adw` : 1 formulaire(s) détecté(s)
- `renault-capture` : 1 formulaire(s) détecté(s)
- `sage-gestion-de-la-paie-hd` : 1 formulaire(s) détecté(s)
- `sauvie-defibrillateurs-en-entreprise` : 1 formulaire(s) détecté(s)
- `toyota-gamme-hybride` : 1 formulaire(s) détecté(s)
- `typ-formulaires-typ-secu-form` : 1 formulaire(s) détecté(s)
- `voiture-nouveau-range-rover` : 2 formulaire(s) détecté(s)
- `voiture-range-rover` : 1 formulaire(s) détecté(s)
- `volvo` : 2 formulaire(s) détecté(s)

Certaines pages sont exclues volontairement du traitement automatique : champs et noms non standards, étapes ou questions répétées, formulaires multiples, anciens SMS ou interfaces spécifiques. Il faut adapter chacune sans écraser son contenu ni perdre ses réponses.

## Tests et limites

```sh
npm ci --prefix tests
npm test --prefix tests
python3 -m unittest discover -s tests -v
```

Le banc contient 306 tests JavaScript avec jsdom et jQuery : il couvre les 49 formulaires équipés, le SMS simulé, les échecs CRM/Sheets, la confirmation avant succès, le honeypot, le consentement, les réponses aux questions, les formId, les redirections connues, ainsi que la soumission jQuery avec le bundle chargé sur les 47 pages adaptées hors références. Le réseau est **mocké**, les parcours visuels et toutes les branches Formly ne sont pas intégralement exécutés : ces tests ne prouvent pas la réception d'un vrai SMS ou lead ni le comportement du domaine déployé.

Avant mise en production : vérifier les formId et leur routage, l'Apps Script et la feuille, les CORS CRM/SMS, les destinations de remerciement, le consentement et GTM, puis réaliser un SMS et un lead réels par famille sur les domaines finaux. Le simulateur local reste présent dans les pages non traitées : il ne démontre pas une livraison réelle.
