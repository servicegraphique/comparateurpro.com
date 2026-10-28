# Audit des fonctionnalités par page

Date de l'audit : 2026-10-28 — branche et fichiers locaux. Génération : `python3 tools/audit_fonctionnalites.py`.

## Résumé

- **133 pages** `*/index.html` examinées ; les pages générées dynamiquement ou en dehors de ce niveau ne sont pas couvertes.
- **49 pages équipées selon les contrôles statiques** : formulaire marqué, modules chargés dans le bon ordre, téléphone lié, code tracking/CRM/Sheets/SMS et chargeur GTM détectés. Elles incluent `LP_reference` et `vehicules-utilitaires`.
- **28 pages avec téléphone détecté mais sans standard complet reconnu** ; cela ne signifie pas nécessairement absence de toute intégration historique.
- **56 autres pages sans téléphone détecté et sans standard complet reconnu** : contenu, qualification, remerciement, préférences, iframes ou autres cas à qualifier.
- **49 pages** avec un chargeur GTM détecté dans une balise script active du HTML (et non seulement dans un commentaire ou un rapport).

Tests exécutés le 28 octobre 2026 sur la version auditée : **308/308 tests JavaScript** et **8/8 tests Python** réussis. Les scénarios JavaScript utilisent jsdom, jQuery et des réponses réseau **simulées** ; ils ne prouvent pas une réception réelle ni la totalité des clics, variantes et parcours. Les 49 bundles ont aussi été chargés avec une soumission jQuery simulée. Les 231 fichiers `script.js`, `lead-handler.js` et `verification-sms.js` ont passé `node --check`. Ces résultats ne préjugent pas des modifications futures.

**Important : aucune page n’est ici déclarée validée en production.** Il faut vérifier les identifiants CRM et leur routage, la feuille Apps Script, les CORS et réponses réelles de l’API SMS, les événements GTM et les leads réels sur les domaines finaux.

- Le succès nécessite une confirmation CRM **ou** Sheets, pas nécessairement les deux. CRM est configuré en `no-cors` sur les 49 pages : un envoi opaque ou beacon est non confirmé. Si Sheets confirme alors que le CRM ne confirme pas, le succès ne prouve pas la réception CRM ; si Sheets échoue, une nouvelle tentative peut créer un doublon sans déduplication serveur.
- La validation SMS vérifie les erreurs et rejette les réponses vides, mais peut accepter un objet JSON non vide sans indicateur positif explicite. Confirmer le contrat réel de l’API avant de conclure que le numéro est vérifié.
- La collecte de tracking est conditionnée par le consentement dans le code ; la présence du conteneur ou d’un événement local ne garantit pas sa configuration ni sa réception dans GTM ou GA4.

## Légende

- **Équipée** : critères statiques ci-dessus satisfaits ; ce n’est pas une preuve de fonctionnement réel.
- **Téléphone à adapter** : au moins un formulaire avec téléphone détecté, sans standard complet reconnu.
- **À qualifier** : aucun formulaire téléphonique détecté ; une qualification, un formulaire e-mail, un tunnel, une iframe ou une page de contenu peuvent nécessiter un autre traitement.
- Colonnes Track, SMS, CRM et Sheets : **code chargé/configuré détecté**, pas une livraison ou vérification réelle ; « non établi » ne veut pas dire qu’aucun code historique n’existe.
- GTM : identifiant d’un chargeur détecté dans le HTML ; « non détecté » n’exclut pas un chargement dynamique ailleurs.
- Le test d’une seule LP ne suffit pas à déclarer conformes ses autres formulaires éventuels ou la page enfant d’une iframe.

## Pages équipées : liste demandée

| Page | formId CRM | GTM |
|---|---|---|
| [`LP_reference`](LP_reference/index.html) | `ADW_LP_VEHICULES_DE_SOCIETE` | GTM-53SH7D7F |
| [`acces-internet-et-telephonie-pro`](acces-internet-et-telephonie-pro/index.html) | `ADW_LP_ACCES_INTERNET_ET_TELEPHONIE_PRO` | GTM-53SH7D7F |
| [`assurance-agriculteur`](assurance-agriculteur/index.html) | `ADW_LP_ASSURANCE_AGRICULTEUR` | GTM-53SH7D7F |
| [`assurance-assurance-professionnelle-iard-cookie`](assurance-assurance-professionnelle-iard-cookie/index.html) | `ADW_LP_ASSURANCE_ASSURANCE_PROFESSIONNELLE_IARD_COOKIE` | GTM-53SH7D7F |
| [`assurance-commerce`](assurance-commerce/index.html) | `ADW_LP_ASSURANCE_COMMERCE` | GTM-WMVZJKS |
| [`assurance-consultants-societe-conseil`](assurance-consultants-societe-conseil/index.html) | `ADW_LP_ASSURANCE_CONSULTANTS_SOCIETE_CONSEIL` | GTM-53SH7D7F |
| [`assurance-estheticienne-institut-beaute`](assurance-estheticienne-institut-beaute/index.html) | `ADW_LP_ASSURANCE_ESTHETICIENNE_INSTITUT_BEAUTE` | GTM-53SH7D7F |
| [`assurance-estheticiennes-instituts-beaute-v1`](assurance-estheticiennes-instituts-beaute-v1/index.html) | `ADW_LP_ASSURANCE_ESTHETICIENNES_INSTITUTS_BEAUTE_V1` | GTM-53SH7D7F |
| [`assurance-iard-v2`](assurance-iard-v2/index.html) | `ADW_LP_ASSURANCE_IARD_V2` | GTM-53SH7D7F |
| [`assurance-marchandise`](assurance-marchandise/index.html) | `ADW_LP_ASSURANCE_MARCHANDISE` | GTM-WMVZJKS |
| [`assurance-multirisques`](assurance-multirisques/index.html) | `ADW_LP_ASSURANCE_MULTIRISQUES` | GTM-53SH7D7F |
| [`assurance-professionnelle-iard`](assurance-professionnelle-iard/index.html) | `ADW_LP_ASSURANCE_PROFESSIONNELLE_IARD` | GTM-53SH7D7F |
| [`assurance-professionnelle-tns-v2`](assurance-professionnelle-tns-v2/index.html) | `ADW_LP_ASSURANCE_PROFESSIONNELLE_TNS_V2` | GTM-WMVZJKS |
| [`assurance-protection-sociale-collective`](assurance-protection-sociale-collective/index.html) | `ADW_LP_ASSURANCE_PROTECTION_SOCIALE_COLLECTIVE` | GTM-53SH7D7F |
| [`assurance-rc-pro`](assurance-rc-pro/index.html) | `ADW_LP_ASSURANCE_RC_PRO` | GTM-53SH7D7F |
| [`assurance-tns`](assurance-tns/index.html) | `ADW_LP_ASSURANCE_TNS` | GTM-53SH7D7F |
| [`assurance-tns-pro-v2-adw`](assurance-tns-pro-v2-adw/index.html) | `ADW_LP_ASSURANCE_TNS_PRO` | GTM-53SH7D7F |
| [`automobile`](automobile/index.html) | `ADW_LP_AUTOMOBILE` | GTM-53SH7D7F |
| [`celebrez-le-noel-des-salaries-avec-kadeos`](celebrez-le-noel-des-salaries-avec-kadeos/index.html) | `ADW_LP_CELEBREZ_LE_NOEL_DES_SALARIES_AVEC_KADEOS` | GTM-53SH7D7F |
| [`complementaire-retraite-tns-v2`](complementaire-retraite-tns-v2/index.html) | `ADW_LP_COMPLEMENTAIRE_RETRAITE_TNS_V2` | GTM-WMVZJKS |
| [`ecomobility`](ecomobility/index.html) | `ADW_LP_ECOMOBILITY` | GTM-53SH7D7F |
| [`edenred-ticket-restaurant-juillet-v1`](edenred-ticket-restaurant-juillet-v1/index.html) | `ADW_LP_EDENRED_TICKET_RESTAURANT_JUILLET_V1` | GTM-53SH7D7F |
| [`energie`](energie/index.html) | `ADW_LP_ENERGIE` | GTM-WMVZJKS |
| [`fiat-pro`](fiat-pro/index.html) | `ADW_LP_FIAT_PRO` | GTM-53SH7D7F |
| [`geolocalisation`](geolocalisation/index.html) | `ADW_LP_GEOLOCALISATION` | GTM-WMVZJKS |
| [`geolocalisation-de-flotte`](geolocalisation-de-flotte/index.html) | `ADW_LP_GEOLOCALISATION_DE_FLOTTE` | GTM-53SH7D7F |
| [`mercedes-benz-mercedes-benz-evito`](mercedes-benz-mercedes-benz-evito/index.html) | `ADW_LP_MERCEDES_BENZ_MERCEDES_BENZ_EVITO` | GTM-53SH7D7F |
| [`mercedes-benz-nouvel-ecitan-fourgon`](mercedes-benz-nouvel-ecitan-fourgon/index.html) | `ADW_LP_MERCEDES_BENZ_NOUVEL_ECITAN_FOURGON` | GTM-53SH7D7F |
| [`mercedes-benz-sprinter`](mercedes-benz-sprinter/index.html) | `ADW_LP_MERCEDES_BENZ_SPRINTER` | GTM-53SH7D7F |
| [`nissan-ariya`](nissan-ariya/index.html) | `ADW_LP_NISSAN_ARIYA` | GTM-53SH7D7F |
| [`nissan-juke`](nissan-juke/index.html) | `ADW_LP_NISSAN_JUKE` | GTM-53SH7D7F |
| [`panneaux-photovoltaiques-energie-solaire`](panneaux-photovoltaiques-energie-solaire/index.html) | `ADW_LP_PANNEAUX_PHOTOVOLTAIQUES_ENERGIE_SOLAIRE` | GTM-WMVZJKS |
| [`securite-professionnels`](securite-professionnels/index.html) | `ADW_LP_SECURITE_PROFESSIONNELS` | GTM-WMVZJKS |
| [`still-manutention`](still-manutention/index.html) | `ADW_LP_STILL_MANUTENTION` | GTM-53SH7D7F |
| [`suivi-de-vehicules`](suivi-de-vehicules/index.html) | `ADW_LP_SUIVI_DE_VEHICULES` | GTM-53SH7D7F |
| [`ticket-restaurant`](ticket-restaurant/index.html) | `ADW_LP_TICKET_RESTAURANT` | GTM-53SH7D7F |
| [`ticket-restaurant-`](ticket-restaurant-/index.html) | `ADW_LP_TICKET_RESTAURANT_VARIANTE` | GTM-53SH7D7F |
| [`ticket-restaurant-septembre`](ticket-restaurant-septembre/index.html) | `ADW_LP_TICKET_RESTAURANT_SEPTEMBRE` | GTM-53SH7D7F |
| [`ticket-restaurant-septembre-btp`](ticket-restaurant-septembre-btp/index.html) | `ADW_LP_TICKET_RESTAURANT_SEPTEMBRE_BTP` | GTM-53SH7D7F |
| [`tns-prevoyance-v2`](tns-prevoyance-v2/index.html) | `ADW_LP_TNS_PREVOYANCE_V2` | GTM-WMVZJKS |
| [`tns-prevoyance-v2-adw-test`](tns-prevoyance-v2-adw-test/index.html) | `ADW_LP_TNS_PREVOYANCE_V2_ADW_TEST` | GTM-WMVZJKS |
| [`too-good-to-go`](too-good-to-go/index.html) | `ADW_LP_TOO_GOOD_TO_GO` | GTM-53SH7D7F |
| [`typ-formulaires-form-typ-vehicules`](typ-formulaires-form-typ-vehicules/index.html) | `ADW_LP_TYP_FORMULAIRES_FORM_TYP_VEHICULES` | GTM-53SH7D7F |
| [`typ-formulaires-typ-caisses-enregistreuse`](typ-formulaires-typ-caisses-enregistreuse/index.html) | `ADW_LP_TYP_FORMULAIRES_TYP_CAISSES_ENREGISTREUSE` | GTM-53SH7D7F |
| [`typ-formulaires-typ-energie-form`](typ-formulaires-typ-energie-form/index.html) | `ADW_LP_TYP_FORMULAIRES_TYP_ENERGIE_FORM` | GTM-53SH7D7F |
| [`typ-formulaires-typ-panneaux-form`](typ-formulaires-typ-panneaux-form/index.html) | `ADW_LP_TYP_FORMULAIRES_TYP_PANNEAUX_FORM` | GTM-53SH7D7F |
| [`une-rentree-sous-le-signe-du-pouvoir-d-achat`](une-rentree-sous-le-signe-du-pouvoir-d-achat/index.html) | `ADW_LP_UNE_RENTREE_SOUS_LE_SIGNE_DU_POUVOIR_D_ACHAT` | GTM-53SH7D7F |
| [`vehicules-de-societe-hd`](vehicules-de-societe-hd/index.html) | `ADW_LP_VEHICULES_DE_SOCIETE_HD` | GTM-53SH7D7F |
| [`vehicules-utilitaires`](vehicules-utilitaires/index.html) | `ADW_LP_VEHICULES_UTILITAIRES` | GTM-WMVZJKS |

## Détail de toutes les pages

| Page | Statut indicatif | Track | GTM dans HTML | SMS | CRM | Sheets | Notes |
|---|---|---|---|---|---|---|---|
| [`LP_reference`](LP_reference/index.html) | Équipée | code | GTM-53SH7D7F | code | code | code | Configuration et réception à valider |
| [`acces-internet-et-telephonie-pro`](acces-internet-et-telephonie-pro/index.html) | Équipée | code | GTM-53SH7D7F | code | code | code | Configuration et réception à valider |
| [`acces-internet-et-telephonie-pro-v2`](acces-internet-et-telephonie-pro-v2/index.html) | À qualifier | non établi | non détecté | non établi | non établi | non établi | 1 formulaire(s) HTML |
| [`accueil`](accueil/index.html) | À qualifier | non établi | non détecté | non établi | non établi | non établi | 1 formulaire(s) HTML |
| [`alfaromeo-tonale`](alfaromeo-tonale/index.html) | Téléphone à adapter | non établi | non détecté | non établi | non établi | non établi | 1 formulaire(s) téléphone détecté(s) |
| [`alfaromeo-tonale-remerciement`](alfaromeo-tonale-remerciement/index.html) | À qualifier | non établi | non détecté | non établi | non établi | non établi | 0 formulaire(s) HTML |
| [`assurance-agriculteur`](assurance-agriculteur/index.html) | Équipée | code | GTM-53SH7D7F | code | code | code | Configuration et réception à valider |
| [`assurance-agriculteur-v2`](assurance-agriculteur-v2/index.html) | À qualifier | non établi | non détecté | non établi | non établi | non établi | 0 formulaire(s) HTML |
| [`assurance-assurance-professionnelle-iard-cookie`](assurance-assurance-professionnelle-iard-cookie/index.html) | Équipée | code | GTM-53SH7D7F | code | code | code | Configuration et réception à valider |
| [`assurance-assurance-professionnelle-iard-v2`](assurance-assurance-professionnelle-iard-v2/index.html) | À qualifier | non établi | non détecté | non établi | non établi | non établi | 1 formulaire(s) HTML |
| [`assurance-commerce`](assurance-commerce/index.html) | Équipée | code | GTM-WMVZJKS | code | code | code | Configuration et réception à valider |
| [`assurance-consultant-societe-conseil-v2`](assurance-consultant-societe-conseil-v2/index.html) | À qualifier | non établi | non détecté | non établi | non établi | non établi | 0 formulaire(s) HTML; iframe : ../assurance-consultants-societe-conseil/ |
| [`assurance-consultants-societe-conseil`](assurance-consultants-societe-conseil/index.html) | Équipée | code | GTM-53SH7D7F | code | code | code | Configuration et réception à valider |
| [`assurance-estheticienne-institut-beaute`](assurance-estheticienne-institut-beaute/index.html) | Équipée | code | GTM-53SH7D7F | code | code | code | Configuration et réception à valider |
| [`assurance-estheticiennes-institut-beaute`](assurance-estheticiennes-institut-beaute/index.html) | Téléphone à adapter | non établi | non détecté | non établi | non établi | non établi | 1 formulaire(s) téléphone détecté(s) |
| [`assurance-estheticiennes-instituts-beaute`](assurance-estheticiennes-instituts-beaute/index.html) | À qualifier | non établi | non détecté | non établi | non établi | non établi | 0 formulaire(s) HTML; iframe : ../assurance-estheticiennes-institut-beaute/ |
| [`assurance-estheticiennes-instituts-beaute-v1`](assurance-estheticiennes-instituts-beaute-v1/index.html) | Équipée | code | GTM-53SH7D7F | code | code | code | Configuration et réception à valider |
| [`assurance-iard-v2`](assurance-iard-v2/index.html) | Équipée | code | GTM-53SH7D7F | code | code | code | Configuration et réception à valider |
| [`assurance-marchandise`](assurance-marchandise/index.html) | Équipée | code | GTM-WMVZJKS | code | code | code | Configuration et réception à valider |
| [`assurance-multirisques`](assurance-multirisques/index.html) | Équipée | code | GTM-53SH7D7F | code | code | code | Configuration et réception à valider |
| [`assurance-professionnelle-iard`](assurance-professionnelle-iard/index.html) | Équipée | code | GTM-53SH7D7F | code | code | code | Configuration et réception à valider |
| [`assurance-professionnelle-tns-v2`](assurance-professionnelle-tns-v2/index.html) | Équipée | code | GTM-WMVZJKS | code | code | code | Configuration et réception à valider |
| [`assurance-protection-sociale-collective`](assurance-protection-sociale-collective/index.html) | Équipée | code | GTM-53SH7D7F | code | code | code | Configuration et réception à valider |
| [`assurance-protection-sociale-collective-v4`](assurance-protection-sociale-collective-v4/index.html) | À qualifier | non établi | non détecté | non établi | non établi | non établi | 1 formulaire(s) HTML |
| [`assurance-rc-pro`](assurance-rc-pro/index.html) | Équipée | code | GTM-53SH7D7F | code | code | code | Configuration et réception à valider |
| [`assurance-test-telephone`](assurance-test-telephone/index.html) | Téléphone à adapter | non établi | non détecté | non établi | non établi | non établi | 1 formulaire(s) téléphone détecté(s) |
| [`assurance-tns`](assurance-tns/index.html) | Équipée | code | GTM-53SH7D7F | code | code | code | Configuration et réception à valider |
| [`assurance-tns-pro-v2-adw`](assurance-tns-pro-v2-adw/index.html) | Équipée | code | GTM-53SH7D7F | code | code | code | Configuration et réception à valider |
| [`assurances-multirisques-v2`](assurances-multirisques-v2/index.html) | À qualifier | non établi | non détecté | non établi | non établi | non établi | 1 formulaire(s) HTML |
| [`assurances-professionnelles`](assurances-professionnelles/index.html) | Téléphone à adapter | non établi | non détecté | non établi | non établi | non établi | 1 formulaire(s) téléphone détecté(s) |
| [`automobile`](automobile/index.html) | Équipée | code | GTM-53SH7D7F | code | code | code | Configuration et réception à valider |
| [`ayvens-france`](ayvens-france/index.html) | Téléphone à adapter | non établi | non détecté | non établi | non établi | non établi | 1 formulaire(s) téléphone détecté(s) |
| [`canal`](canal/index.html) | À qualifier | non établi | non détecté | non établi | non établi | non établi | 2 formulaire(s) HTML |
| [`cartes-carburant`](cartes-carburant/index.html) | Téléphone à adapter | non établi | non détecté | non établi | non établi | non établi | 1 formulaire(s) téléphone détecté(s) |
| [`celebrez-le-noel-des-salaries-avec-kadeos`](celebrez-le-noel-des-salaries-avec-kadeos/index.html) | Équipée | code | GTM-53SH7D7F | code | code | code | Configuration et réception à valider |
| [`complementaire-retraite-tns-v2`](complementaire-retraite-tns-v2/index.html) | Équipée | code | GTM-WMVZJKS | code | code | code | Configuration et réception à valider |
| [`dacia-jogger`](dacia-jogger/index.html) | Téléphone à adapter | non établi | non détecté | non établi | non établi | non établi | 1 formulaire(s) téléphone détecté(s) |
| [`ecomobility`](ecomobility/index.html) | Équipée | code | GTM-53SH7D7F | code | code | code | Configuration et réception à valider |
| [`edenred-kadeos`](edenred-kadeos/index.html) | Téléphone à adapter | non établi | non détecté | non établi | non établi | non établi | 1 formulaire(s) téléphone détecté(s) |
| [`edenred-restaurant-v2`](edenred-restaurant-v2/index.html) | À qualifier | non établi | non détecté | non établi | non établi | non établi | 1 formulaire(s) HTML |
| [`edenred-ticket-restaurant-juillet-v1`](edenred-ticket-restaurant-juillet-v1/index.html) | Équipée | code | GTM-53SH7D7F | code | code | code | Configuration et réception à valider |
| [`edenred-titre-restaurant-v2`](edenred-titre-restaurant-v2/index.html) | À qualifier | non établi | non détecté | non établi | non établi | non établi | 1 formulaire(s) HTML |
| [`edenred-typ`](edenred-typ/index.html) | À qualifier | non établi | non détecté | non établi | non établi | non établi | 0 formulaire(s) HTML |
| [`energie`](energie/index.html) | Équipée | code | GTM-WMVZJKS | code | code | code | Configuration et réception à valider |
| [`energie-v2`](energie-v2/index.html) | À qualifier | non établi | non détecté | non établi | non établi | non établi | 1 formulaire(s) HTML |
| [`fiat-pro`](fiat-pro/index.html) | Équipée | code | GTM-53SH7D7F | code | code | code | Configuration et réception à valider |
| [`form-panneaux-photovoltaiques`](form-panneaux-photovoltaiques/index.html) | À qualifier | non établi | non détecté | non établi | non établi | non établi | 1 formulaire(s) HTML |
| [`form-vehicules-utilitaires`](form-vehicules-utilitaires/index.html) | À qualifier | non établi | non détecté | non établi | non établi | non établi | 1 formulaire(s) HTML |
| [`formulaire`](formulaire/index.html) | À qualifier | non établi | non détecté | non établi | non établi | non établi | 0 formulaire(s) HTML |
| [`formulaire-globale`](formulaire-globale/index.html) | Téléphone à adapter | non établi | non détecté | non établi | non établi | non établi | 1 formulaire(s) téléphone détecté(s) |
| [`gamme-de-rayonnage-actiflip-hd`](gamme-de-rayonnage-actiflip-hd/index.html) | Téléphone à adapter | non établi | non détecté | non établi | non établi | non établi | 1 formulaire(s) téléphone détecté(s) |
| [`gamme-de-rayonnage-actiflip-v4`](gamme-de-rayonnage-actiflip-v4/index.html) | Téléphone à adapter | non établi | non détecté | non établi | non établi | non établi | 1 formulaire(s) téléphone détecté(s) |
| [`geo`](geo/index.html) | À qualifier | non établi | non détecté | non établi | non établi | non établi | 0 formulaire(s) HTML |
| [`geolocalisation`](geolocalisation/index.html) | Équipée | code | GTM-WMVZJKS | code | code | code | Configuration et réception à valider |
| [`geolocalisation-de-flotte`](geolocalisation-de-flotte/index.html) | Équipée | code | GTM-53SH7D7F | code | code | code | Configuration et réception à valider |
| [`geolocalisation-v2`](geolocalisation-v2/index.html) | À qualifier | non établi | non détecté | non établi | non établi | non établi | 1 formulaire(s) HTML |
| [`hyundai-kona-electric-nouvelle-generation`](hyundai-kona-electric-nouvelle-generation/index.html) | À qualifier | non établi | non détecté | non établi | non établi | non établi | 1 formulaire(s) HTML |
| [`hyundai-tucson`](hyundai-tucson/index.html) | À qualifier | non établi | non détecté | non établi | non établi | non établi | 1 formulaire(s) HTML |
| [`intuis`](intuis/index.html) | Téléphone à adapter | non établi | non détecté | non établi | non établi | non établi | 1 formulaire(s) téléphone détecté(s) |
| [`lexus-lbx`](lexus-lbx/index.html) | Téléphone à adapter | non établi | non détecté | non établi | non établi | non établi | 1 formulaire(s) téléphone détecté(s) |
| [`lexus-lbx-2`](lexus-lbx-2/index.html) | Téléphone à adapter | non établi | non détecté | non établi | non établi | non établi | 2 formulaire(s) téléphone détecté(s) |
| [`mentions-legales`](mentions-legales/index.html) | À qualifier | non établi | non détecté | non établi | non établi | non établi | 0 formulaire(s) HTML |
| [`mercedes-benz-mercedes-benz-evito`](mercedes-benz-mercedes-benz-evito/index.html) | Équipée | code | GTM-53SH7D7F | code | code | code | Configuration et réception à valider |
| [`mercedes-benz-nouvel-ecitan-fourgon`](mercedes-benz-nouvel-ecitan-fourgon/index.html) | Équipée | code | GTM-53SH7D7F | code | code | code | Configuration et réception à valider |
| [`mercedes-benz-sprinter`](mercedes-benz-sprinter/index.html) | Équipée | code | GTM-53SH7D7F | code | code | code | Configuration et réception à valider |
| [`mercedes-vous-remercie`](mercedes-vous-remercie/index.html) | À qualifier | non établi | non détecté | non établi | non établi | non établi | 0 formulaire(s) HTML |
| [`mitsubishi-fuso`](mitsubishi-fuso/index.html) | Téléphone à adapter | non établi | non détecté | non établi | non établi | non établi | 1 formulaire(s) téléphone détecté(s) |
| [`mitsubishi-fuso-remerciement`](mitsubishi-fuso-remerciement/index.html) | À qualifier | non établi | non détecté | non établi | non établi | non établi | 0 formulaire(s) HTML |
| [`nettoyage-locaux-professionnels`](nettoyage-locaux-professionnels/index.html) | À qualifier | non établi | non détecté | non établi | non établi | non établi | 0 formulaire(s) HTML |
| [`nissan-ariya`](nissan-ariya/index.html) | Équipée | code | GTM-53SH7D7F | code | code | code | Configuration et réception à valider |
| [`nissan-juke`](nissan-juke/index.html) | Équipée | code | GTM-53SH7D7F | code | code | code | Configuration et réception à valider |
| [`panneaux-photovoltaiques-energie-solaire`](panneaux-photovoltaiques-energie-solaire/index.html) | Équipée | code | GTM-WMVZJKS | code | code | code | Configuration et réception à valider |
| [`panneaux-photovoltaiques-panneaux-photovoltaique-valider`](panneaux-photovoltaiques-panneaux-photovoltaique-valider/index.html) | À qualifier | non établi | non détecté | non établi | non établi | non établi | 0 formulaire(s) HTML |
| [`paritel`](paritel/index.html) | Téléphone à adapter | non établi | non détecté | non établi | non établi | non établi | 1 formulaire(s) téléphone détecté(s) |
| [`paritel-typ`](paritel-typ/index.html) | À qualifier | non établi | non détecté | non établi | non établi | non établi | 0 formulaire(s) HTML |
| [`paritel-vous-rembourse`](paritel-vous-rembourse/index.html) | Téléphone à adapter | non établi | non détecté | non établi | non établi | non établi | 1 formulaire(s) téléphone détecté(s) |
| [`paritel-vous-rembourse-v2`](paritel-vous-rembourse-v2/index.html) | À qualifier | non établi | non détecté | non établi | non établi | non établi | 1 formulaire(s) HTML |
| [`politique-de-confidentialite-donnees-personnelles`](politique-de-confidentialite-donnees-personnelles/index.html) | À qualifier | non établi | non détecté | non établi | non établi | non établi | 0 formulaire(s) HTML |
| [`primagaz`](primagaz/index.html) | Téléphone à adapter | non établi | non détecté | non établi | non établi | non établi | 1 formulaire(s) téléphone détecté(s) |
| [`primagaz-obtenez-votre-gaz-propane-a-prix-fixe`](primagaz-obtenez-votre-gaz-propane-a-prix-fixe/index.html) | Téléphone à adapter | non établi | non détecté | non établi | non établi | non établi | 1 formulaire(s) téléphone détecté(s) |
| [`primagaz-v2`](primagaz-v2/index.html) | À qualifier | non établi | non détecté | non établi | non établi | non établi | 1 formulaire(s) HTML |
| [`radius-remerciement`](radius-remerciement/index.html) | À qualifier | non établi | non détecté | non établi | non établi | non établi | 0 formulaire(s) HTML |
| [`radius-telematics-typ`](radius-telematics-typ/index.html) | À qualifier | non établi | non détecté | non établi | non établi | non établi | 0 formulaire(s) HTML |
| [`rc-pro-consultant-conseil-adw`](rc-pro-consultant-conseil-adw/index.html) | Téléphone à adapter | non établi | non détecté | non établi | non établi | non établi | 1 formulaire(s) téléphone détecté(s) |
| [`remerciement-carte-cadeau`](remerciement-carte-cadeau/index.html) | À qualifier | non établi | non détecté | non établi | non établi | non établi | 1 formulaire(s) HTML |
| [`remerciement-panneaux-solaire`](remerciement-panneaux-solaire/index.html) | À qualifier | non établi | non détecté | non établi | non établi | non établi | 1 formulaire(s) HTML |
| [`remerciement-ticket-restaurant`](remerciement-ticket-restaurant/index.html) | À qualifier | non établi | non détecté | non établi | non établi | non établi | 1 formulaire(s) HTML |
| [`remerciement-ticket-restaurant-v2`](remerciement-ticket-restaurant-v2/index.html) | À qualifier | non établi | non détecté | non établi | non établi | non établi | 1 formulaire(s) HTML |
| [`remerciements-panneaux-solaires`](remerciements-panneaux-solaires/index.html) | À qualifier | non établi | non détecté | non établi | non établi | non établi | 1 formulaire(s) HTML |
| [`renault-capture`](renault-capture/index.html) | Téléphone à adapter | non établi | non détecté | non établi | non établi | non établi | 1 formulaire(s) téléphone détecté(s) |
| [`sage-gestion-de-la-paie-hd`](sage-gestion-de-la-paie-hd/index.html) | Téléphone à adapter | non établi | non détecté | non établi | non établi | non établi | 1 formulaire(s) téléphone détecté(s) |
| [`sage-gestion-de-la-paie-hd-v4`](sage-gestion-de-la-paie-hd-v4/index.html) | À qualifier | non établi | non détecté | non établi | non établi | non établi | 1 formulaire(s) HTML |
| [`sauvie-defibrillateurs-en-entreprise`](sauvie-defibrillateurs-en-entreprise/index.html) | Téléphone à adapter | non établi | non détecté | non établi | non établi | non établi | 1 formulaire(s) téléphone détecté(s) |
| [`securite-pro-v2`](securite-pro-v2/index.html) | À qualifier | non établi | non détecté | non établi | non établi | non établi | 1 formulaire(s) HTML |
| [`securite-professionnels`](securite-professionnels/index.html) | Équipée | code | GTM-WMVZJKS | code | code | code | Configuration et réception à valider |
| [`site`](site/index.html) | À qualifier | non établi | non détecté | non établi | non établi | non établi | 0 formulaire(s) HTML |
| [`solutions-cles`](solutions-cles/index.html) | À qualifier | non établi | non détecté | non établi | non établi | non établi | 0 formulaire(s) HTML |
| [`solutions-industrielles-cles-en-main`](solutions-industrielles-cles-en-main/index.html) | À qualifier | non établi | non détecté | non établi | non établi | non établi | 0 formulaire(s) HTML |
| [`still-manutention`](still-manutention/index.html) | Équipée | code | GTM-53SH7D7F | code | code | code | Configuration et réception à valider |
| [`suivi-de-vehicules`](suivi-de-vehicules/index.html) | Équipée | code | GTM-53SH7D7F | code | code | code | Configuration et réception à valider |
| [`template-2`](template-2/index.html) | À qualifier | non établi | non détecté | non établi | non établi | non établi | 1 formulaire(s) HTML |
| [`ticket-restaurant`](ticket-restaurant/index.html) | Équipée | code | GTM-53SH7D7F | code | code | code | Configuration et réception à valider |
| [`ticket-restaurant-`](ticket-restaurant-/index.html) | Équipée | code | GTM-53SH7D7F | code | code | code | Configuration et réception à valider |
| [`ticket-restaurant-septembre`](ticket-restaurant-septembre/index.html) | Équipée | code | GTM-53SH7D7F | code | code | code | Configuration et réception à valider |
| [`ticket-restaurant-septembre-btp`](ticket-restaurant-septembre-btp/index.html) | Équipée | code | GTM-53SH7D7F | code | code | code | Configuration et réception à valider |
| [`ticket-restaurant-v2`](ticket-restaurant-v2/index.html) | À qualifier | non établi | non détecté | non établi | non établi | non établi | 1 formulaire(s) HTML |
| [`tns-prevoyance-v2`](tns-prevoyance-v2/index.html) | Équipée | code | GTM-WMVZJKS | code | code | code | Configuration et réception à valider |
| [`tns-prevoyance-v2-adw-test`](tns-prevoyance-v2-adw-test/index.html) | Équipée | code | GTM-WMVZJKS | code | code | code | Configuration et réception à valider |
| [`too-good-to-go`](too-good-to-go/index.html) | Équipée | code | GTM-53SH7D7F | code | code | code | Configuration et réception à valider |
| [`toyota-gamme-hybride`](toyota-gamme-hybride/index.html) | Téléphone à adapter | non établi | non détecté | non établi | non établi | non établi | 1 formulaire(s) téléphone détecté(s) |
| [`typ-categ`](typ-categ/index.html) | À qualifier | non établi | non détecté | non établi | non établi | non établi | 0 formulaire(s) HTML |
| [`typ-categories`](typ-categories/index.html) | À qualifier | non établi | non détecté | non établi | non établi | non établi | 0 formulaire(s) HTML; iframe : ../typ-formulaires-vehicules-thank-you-page/, ../typ-formulaires-securite-thank-you-page/, ../typ-formulaires-energie-thank-you-page/, ../typ-formulaires-panneaux-thank-you-page/, ../typ-formulaires-caisses-thank-you-page/, ../typ-formulaires-typ-log-entreprise/ |
| [`typ-energie`](typ-energie/index.html) | À qualifier | non établi | non détecté | non établi | non établi | non établi | 1 formulaire(s) HTML |
| [`typ-formulaires-caisses-thank-you-page`](typ-formulaires-caisses-thank-you-page/index.html) | À qualifier | non établi | non détecté | non établi | non établi | non établi | 1 formulaire(s) HTML |
| [`typ-formulaires-energie-thank-you-page`](typ-formulaires-energie-thank-you-page/index.html) | À qualifier | non établi | non détecté | non établi | non établi | non établi | 1 formulaire(s) HTML |
| [`typ-formulaires-form-typ-vehicules`](typ-formulaires-form-typ-vehicules/index.html) | Équipée | code | GTM-53SH7D7F | code | code | code | Configuration et réception à valider |
| [`typ-formulaires-panneaux-photovoltaiques`](typ-formulaires-panneaux-photovoltaiques/index.html) | À qualifier | non établi | non détecté | non établi | non établi | non établi | 1 formulaire(s) HTML |
| [`typ-formulaires-panneaux-thank-you-page`](typ-formulaires-panneaux-thank-you-page/index.html) | À qualifier | non établi | non détecté | non établi | non établi | non établi | 1 formulaire(s) HTML |
| [`typ-formulaires-securite-thank-you-page`](typ-formulaires-securite-thank-you-page/index.html) | À qualifier | non établi | non détecté | non établi | non établi | non établi | 1 formulaire(s) HTML |
| [`typ-formulaires-typ-caisses-enregistreuse`](typ-formulaires-typ-caisses-enregistreuse/index.html) | Équipée | code | GTM-53SH7D7F | code | code | code | Configuration et réception à valider |
| [`typ-formulaires-typ-energie-form`](typ-formulaires-typ-energie-form/index.html) | Équipée | code | GTM-53SH7D7F | code | code | code | Configuration et réception à valider |
| [`typ-formulaires-typ-log-entreprise`](typ-formulaires-typ-log-entreprise/index.html) | À qualifier | non établi | non détecté | non établi | non établi | non établi | 1 formulaire(s) HTML |
| [`typ-formulaires-typ-panneaux-form`](typ-formulaires-typ-panneaux-form/index.html) | Équipée | code | GTM-53SH7D7F | code | code | code | Configuration et réception à valider |
| [`typ-formulaires-typ-secu-form`](typ-formulaires-typ-secu-form/index.html) | Téléphone à adapter | non établi | non détecté | non établi | non établi | non établi | 1 formulaire(s) téléphone détecté(s) |
| [`typ-formulaires-vehicules-thank-you-page`](typ-formulaires-vehicules-thank-you-page/index.html) | À qualifier | non établi | non détecté | non établi | non établi | non établi | 1 formulaire(s) HTML |
| [`typ-ticket-restaurant`](typ-ticket-restaurant/index.html) | À qualifier | non établi | non détecté | non établi | non établi | non établi | 1 formulaire(s) HTML |
| [`une-rentree-sous-le-signe-du-pouvoir-d-achat`](une-rentree-sous-le-signe-du-pouvoir-d-achat/index.html) | Équipée | code | GTM-53SH7D7F | code | code | code | Configuration et réception à valider |
| [`vehicules-de-societe-hd`](vehicules-de-societe-hd/index.html) | Équipée | code | GTM-53SH7D7F | code | code | code | Configuration et réception à valider |
| [`vehicules-professionnel-v2`](vehicules-professionnel-v2/index.html) | À qualifier | non établi | non détecté | non établi | non établi | non établi | 1 formulaire(s) HTML |
| [`vehicules-utilitaires`](vehicules-utilitaires/index.html) | Équipée | code | GTM-WMVZJKS | code | code | code | Configuration et réception à valider |
| [`voiture-nouveau-range-rover`](voiture-nouveau-range-rover/index.html) | Téléphone à adapter | non établi | non détecté | non établi | non établi | non établi | 2 formulaire(s) téléphone détecté(s) |
| [`voiture-range-rover`](voiture-range-rover/index.html) | Téléphone à adapter | non établi | non détecté | non établi | non établi | non établi | 1 formulaire(s) téléphone détecté(s) |
| [`volvo`](volvo/index.html) | Téléphone à adapter | non établi | non détecté | non établi | non établi | non établi | 2 formulaire(s) téléphone détecté(s) |
