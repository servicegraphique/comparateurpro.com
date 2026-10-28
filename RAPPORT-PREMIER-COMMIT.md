# Réexamen des dossiers depuis le premier commit

Référence historique : premier commit `5b7b2e6`, état comparé `88adabd` (après fusion des PR précédentes). La colonne historique ne reflète pas les modifications locales en cours ; celles-ci sont décrites dans la colonne statut.

Sur **133 dossiers avec `index.html`**, 84 étaient inchangés depuis le premier commit à l’état comparé, 47 avaient été modifiés et 2 avaient été ajoutés après celui-ci. Les dossiers techniques `tests` et `tools` ne sont pas des pages.

**Travail effectué précédemment :** correction de `assurance-estheticiennes-institut-beaute` et de son parent iframe `assurance-estheticiennes-instituts-beaute`. La page de capture conserve son formulaire, ses questions, ses destinations et son `formId` existant `ADW_LP_ASSURANCE_CONSULTANT` ; cet identifiant atypique doit être confirmé auprès du CRM. Le code émet la conversion et montre le succès uniquement après confirmation CRM CORS ou Google Sheets, pas nécessairement les deux.

**Six pages supplémentaires** ont uniquement récupéré leur conteneur GTM identifié dans leur rapport d’origine : `assurance-agriculteur-v2`, `assurance-assurance-professionnelle-iard-v2`, `assurance-protection-sociale-collective-v4`, `assurances-multirisques-v2`, `energie-v2` et `geolocalisation-v2`. Le Consent Mode par défaut précède le chargeur ; les tags configurés dans les conteneurs et la réception effective doivent être contrôlés. Cette intervention ne rend pas leurs formulaires conformes et ne prouve aucune livraison de lead.

**Travail non terminé : 20 pages avec téléphone détecté restent à adapter.** L’utilisateur a défini pour chaque page `ADW-` suivi du nom du dossier comme formId et les URL CRM et Google Sheets des LP de référence ; ces configurations sont renseignées dans `CONFIGURATIONS-CRM-A-COMPLETER.csv`. Sept formulaires ont été adaptés dans cette branche ; les autres ne sont pas encore équipés de ces intégrations. Le chargeur `GTM-53SH7D7F` de référence a été installé sur les 27 pages selon le choix précédent de l’utilisateur, après le Consent Mode par défaut ; les tags configurés et leur déclenchement doivent être vérifiés. Cette seule installation ne valide ni le SMS ni le CRM, Sheets ou les conversions. Les autres pages comprennent notamment des remerciements et des étapes de qualification à examiner individuellement.

Le code corrigé retire le simulateur local de faux succès, vérifie les réponses et la fraîcheur des requêtes SMS, filtre la catégorie URL selon le consentement et rétablit GTM `GTM-53SH7D7F` d’après le rapport de conversion. Le relais iframe ne fait confiance qu’à `https://www.comparateurpro.fr` et au domaine canonique de la page parente ; son déploiement, le chemin de l’iframe, les CORS et son fonctionnement réel doivent être vérifiés sur le domaine final.

Les tests utilisent des réponses simulées : aucune réception réelle SMS, CRM, Sheets ou GTM n’a été vérifiée. Le mode CRM `no-cors` ne confirme pas la réception et peut entraîner des doublons si Sheets échoue et que l’utilisateur réessaie. La réponse SMS JSON non vide peut encore être acceptée sans indicateur positif explicite : contrat API réel à confirmer.

## Pages avec téléphone encore à adapter

- `alfaromeo-tonale` (1 formulaire(s) détecté(s))
- `assurance-test-telephone` (1 formulaire(s) détecté(s))
- `assurances-professionnelles` (1 formulaire(s) détecté(s))
- `cartes-carburant` (1 formulaire(s) détecté(s))
- `edenred-kadeos` (1 formulaire(s) détecté(s))
- `formulaire-globale` (1 formulaire(s) détecté(s))
- `gamme-de-rayonnage-actiflip-hd` (1 formulaire(s) détecté(s))
- `gamme-de-rayonnage-actiflip-v4` (1 formulaire(s) détecté(s))
- `lexus-lbx` (1 formulaire(s) détecté(s))
- `lexus-lbx-2` (2 formulaire(s) détecté(s))
- `paritel` (1 formulaire(s) détecté(s))
- `paritel-vous-rembourse` (1 formulaire(s) détecté(s))
- `primagaz-obtenez-votre-gaz-propane-a-prix-fixe` (1 formulaire(s) détecté(s))
- `rc-pro-consultant-conseil-adw` (1 formulaire(s) détecté(s))
- `sauvie-defibrillateurs-en-entreprise` (1 formulaire(s) détecté(s))
- `toyota-gamme-hybride` (1 formulaire(s) détecté(s))
- `typ-formulaires-typ-secu-form` (1 formulaire(s) détecté(s))
- `voiture-nouveau-range-rover` (2 formulaire(s) détecté(s))
- `voiture-range-rover` (1 formulaire(s) détecté(s))
- `volvo` (2 formulaire(s) détecté(s))

## Détail de tous les dossiers de pages

L’historique est basé sur la comparaison Git du **dossier entier** ; l’analyse des formulaires et des iframes est statique et ne couvre pas les formulaires injectés dynamiquement.

| Dossier | Historique avant ce travail | Statut et action |
|---|---|---|
| [`LP_reference`](LP_reference/index.html) | Ajouté après premier commit | Capture équipée précédemment ; validation réelle requise |
| [`acces-internet-et-telephonie-pro`](acces-internet-et-telephonie-pro/index.html) | Modifié après premier commit | Capture équipée précédemment ; validation réelle requise |
| [`acces-internet-et-telephonie-pro-v2`](acces-internet-et-telephonie-pro-v2/index.html) | Inchangé au premier commit | Autre formulaire ou étape à qualifier : sans coordonnées détectées / à qualifier |
| [`accueil`](accueil/index.html) | Inchangé au premier commit | Autre formulaire ou étape à qualifier : sans coordonnées détectées / à qualifier |
| [`alfaromeo-tonale`](alfaromeo-tonale/index.html) | Inchangé au premier commit | Capture téléphone à adapter (1 formulaire(s)); GTM de référence installé, configuration à valider |
| [`alfaromeo-tonale-remerciement`](alfaromeo-tonale-remerciement/index.html) | Inchangé au premier commit | Aucun formulaire HTML détecté ; rôle à vérifier |
| [`assurance-agriculteur`](assurance-agriculteur/index.html) | Modifié après premier commit | Capture équipée précédemment ; validation réelle requise |
| [`assurance-agriculteur-v2`](assurance-agriculteur-v2/index.html) | Inchangé au premier commit | Aucun formulaire HTML détecté ; rôle à vérifier; chargeur GTM d’origine rétabli uniquement — configuration et réception à vérifier |
| [`assurance-assurance-professionnelle-iard-cookie`](assurance-assurance-professionnelle-iard-cookie/index.html) | Modifié après premier commit | Capture équipée précédemment ; validation réelle requise |
| [`assurance-assurance-professionnelle-iard-v2`](assurance-assurance-professionnelle-iard-v2/index.html) | Inchangé au premier commit | Autre formulaire ou étape à qualifier : sans coordonnées détectées / à qualifier; chargeur GTM d’origine rétabli uniquement — configuration et réception à vérifier |
| [`assurance-commerce`](assurance-commerce/index.html) | Modifié après premier commit | Capture équipée précédemment ; validation réelle requise |
| [`assurance-consultant-societe-conseil-v2`](assurance-consultant-societe-conseil-v2/index.html) | Inchangé au premier commit | Iframe à examiner : ../assurance-consultants-societe-conseil/ |
| [`assurance-consultants-societe-conseil`](assurance-consultants-societe-conseil/index.html) | Modifié après premier commit | Capture équipée précédemment ; validation réelle requise |
| [`assurance-estheticienne-institut-beaute`](assurance-estheticienne-institut-beaute/index.html) | Modifié après premier commit | Capture équipée précédemment ; validation réelle requise |
| [`assurance-estheticiennes-institut-beaute`](assurance-estheticiennes-institut-beaute/index.html) | Inchangé au premier commit | Capture spécifique corrigée dans cette branche ; validation réelle requise |
| [`assurance-estheticiennes-instituts-beaute`](assurance-estheticiennes-instituts-beaute/index.html) | Inchangé au premier commit | Page parente iframe : relais corrigé ; parcours réel à valider |
| [`assurance-estheticiennes-instituts-beaute-v1`](assurance-estheticiennes-instituts-beaute-v1/index.html) | Modifié après premier commit | Capture équipée précédemment ; validation réelle requise |
| [`assurance-iard-v2`](assurance-iard-v2/index.html) | Modifié après premier commit | Capture équipée précédemment ; validation réelle requise |
| [`assurance-marchandise`](assurance-marchandise/index.html) | Modifié après premier commit | Capture équipée précédemment ; validation réelle requise |
| [`assurance-multirisques`](assurance-multirisques/index.html) | Modifié après premier commit | Capture équipée précédemment ; validation réelle requise |
| [`assurance-professionnelle-iard`](assurance-professionnelle-iard/index.html) | Modifié après premier commit | Capture équipée précédemment ; validation réelle requise |
| [`assurance-professionnelle-tns-v2`](assurance-professionnelle-tns-v2/index.html) | Modifié après premier commit | Capture équipée précédemment ; validation réelle requise |
| [`assurance-protection-sociale-collective`](assurance-protection-sociale-collective/index.html) | Modifié après premier commit | Capture équipée précédemment ; validation réelle requise |
| [`assurance-protection-sociale-collective-v4`](assurance-protection-sociale-collective-v4/index.html) | Inchangé au premier commit | Autre formulaire ou étape à qualifier : sans coordonnées détectées / à qualifier; chargeur GTM d’origine rétabli uniquement — configuration et réception à vérifier |
| [`assurance-rc-pro`](assurance-rc-pro/index.html) | Modifié après premier commit | Capture équipée précédemment ; validation réelle requise |
| [`assurance-test-telephone`](assurance-test-telephone/index.html) | Inchangé au premier commit | Capture téléphone à adapter (1 formulaire(s)); GTM de référence installé, configuration à valider |
| [`assurance-tns`](assurance-tns/index.html) | Modifié après premier commit | Capture équipée précédemment ; validation réelle requise |
| [`assurance-tns-pro-v2-adw`](assurance-tns-pro-v2-adw/index.html) | Modifié après premier commit | Capture équipée précédemment ; validation réelle requise |
| [`assurances-multirisques-v2`](assurances-multirisques-v2/index.html) | Inchangé au premier commit | Autre formulaire ou étape à qualifier : sans coordonnées détectées / à qualifier; chargeur GTM d’origine rétabli uniquement — configuration et réception à vérifier |
| [`assurances-professionnelles`](assurances-professionnelles/index.html) | Inchangé au premier commit | Capture téléphone à adapter (1 formulaire(s)); GTM de référence installé, configuration à valider |
| [`automobile`](automobile/index.html) | Modifié après premier commit | Capture équipée précédemment ; validation réelle requise |
| [`ayvens-france`](ayvens-france/index.html) | Inchangé au premier commit | Capture équipée dans cette branche ; formId ADW-ayvens-france ; validation réelle requise |
| [`canal`](canal/index.html) | Inchangé au premier commit | Autre formulaire ou étape à qualifier : sans coordonnées détectées / à qualifier |
| [`cartes-carburant`](cartes-carburant/index.html) | Inchangé au premier commit | Capture téléphone à adapter (1 formulaire(s)); GTM de référence installé, configuration à valider |
| [`celebrez-le-noel-des-salaries-avec-kadeos`](celebrez-le-noel-des-salaries-avec-kadeos/index.html) | Modifié après premier commit | Capture équipée précédemment ; validation réelle requise |
| [`complementaire-retraite-tns-v2`](complementaire-retraite-tns-v2/index.html) | Modifié après premier commit | Capture équipée précédemment ; validation réelle requise |
| [`dacia-jogger`](dacia-jogger/index.html) | Inchangé au premier commit | Capture équipée dans cette branche ; formId ADW-dacia-jogger ; validation réelle requise |
| [`ecomobility`](ecomobility/index.html) | Modifié après premier commit | Capture équipée précédemment ; validation réelle requise |
| [`edenred-kadeos`](edenred-kadeos/index.html) | Inchangé au premier commit | Capture téléphone à adapter (1 formulaire(s)); GTM de référence installé, configuration à valider |
| [`edenred-restaurant-v2`](edenred-restaurant-v2/index.html) | Inchangé au premier commit | Autre formulaire ou étape à qualifier : sans coordonnées détectées / à qualifier |
| [`edenred-ticket-restaurant-juillet-v1`](edenred-ticket-restaurant-juillet-v1/index.html) | Modifié après premier commit | Capture équipée précédemment ; validation réelle requise |
| [`edenred-titre-restaurant-v2`](edenred-titre-restaurant-v2/index.html) | Inchangé au premier commit | Autre formulaire ou étape à qualifier : sans coordonnées détectées / à qualifier |
| [`edenred-typ`](edenred-typ/index.html) | Inchangé au premier commit | Aucun formulaire HTML détecté ; rôle à vérifier |
| [`energie`](energie/index.html) | Modifié après premier commit | Capture équipée précédemment ; validation réelle requise |
| [`energie-v2`](energie-v2/index.html) | Inchangé au premier commit | Autre formulaire ou étape à qualifier : sans coordonnées détectées / à qualifier; chargeur GTM d’origine rétabli uniquement — configuration et réception à vérifier |
| [`fiat-pro`](fiat-pro/index.html) | Modifié après premier commit | Capture équipée précédemment ; validation réelle requise |
| [`form-panneaux-photovoltaiques`](form-panneaux-photovoltaiques/index.html) | Inchangé au premier commit | Autre formulaire ou étape à qualifier : sans coordonnées détectées / à qualifier |
| [`form-vehicules-utilitaires`](form-vehicules-utilitaires/index.html) | Inchangé au premier commit | Autre formulaire ou étape à qualifier : sans coordonnées détectées / à qualifier |
| [`formulaire`](formulaire/index.html) | Inchangé au premier commit | Aucun formulaire HTML détecté ; rôle à vérifier |
| [`formulaire-globale`](formulaire-globale/index.html) | Inchangé au premier commit | Capture téléphone à adapter (1 formulaire(s)); GTM de référence installé, configuration à valider |
| [`gamme-de-rayonnage-actiflip-hd`](gamme-de-rayonnage-actiflip-hd/index.html) | Inchangé au premier commit | Capture téléphone à adapter (1 formulaire(s)); GTM de référence installé, configuration à valider |
| [`gamme-de-rayonnage-actiflip-v4`](gamme-de-rayonnage-actiflip-v4/index.html) | Inchangé au premier commit | Capture téléphone à adapter (1 formulaire(s)); GTM de référence installé, configuration à valider |
| [`geo`](geo/index.html) | Inchangé au premier commit | Aucun formulaire HTML détecté ; rôle à vérifier |
| [`geolocalisation`](geolocalisation/index.html) | Modifié après premier commit | Capture équipée précédemment ; validation réelle requise |
| [`geolocalisation-de-flotte`](geolocalisation-de-flotte/index.html) | Modifié après premier commit | Capture équipée précédemment ; validation réelle requise |
| [`geolocalisation-v2`](geolocalisation-v2/index.html) | Inchangé au premier commit | Autre formulaire ou étape à qualifier : sans coordonnées détectées / à qualifier; chargeur GTM d’origine rétabli uniquement — configuration et réception à vérifier |
| [`hyundai-kona-electric-nouvelle-generation`](hyundai-kona-electric-nouvelle-generation/index.html) | Inchangé au premier commit | Autre formulaire ou étape à qualifier : sans coordonnées détectées / à qualifier |
| [`hyundai-tucson`](hyundai-tucson/index.html) | Inchangé au premier commit | Autre formulaire ou étape à qualifier : sans coordonnées détectées / à qualifier |
| [`intuis`](intuis/index.html) | Inchangé au premier commit | Capture équipée dans cette branche ; formId ADW-intuis ; validation réelle requise |
| [`lexus-lbx`](lexus-lbx/index.html) | Inchangé au premier commit | Capture téléphone à adapter (1 formulaire(s)); GTM de référence installé, configuration à valider |
| [`lexus-lbx-2`](lexus-lbx-2/index.html) | Inchangé au premier commit | Capture téléphone à adapter (2 formulaire(s)); GTM de référence installé, configuration à valider |
| [`mentions-legales`](mentions-legales/index.html) | Inchangé au premier commit | Aucun formulaire HTML détecté ; rôle à vérifier |
| [`mercedes-benz-mercedes-benz-evito`](mercedes-benz-mercedes-benz-evito/index.html) | Modifié après premier commit | Capture équipée précédemment ; validation réelle requise |
| [`mercedes-benz-nouvel-ecitan-fourgon`](mercedes-benz-nouvel-ecitan-fourgon/index.html) | Modifié après premier commit | Capture équipée précédemment ; validation réelle requise |
| [`mercedes-benz-sprinter`](mercedes-benz-sprinter/index.html) | Modifié après premier commit | Capture équipée précédemment ; validation réelle requise |
| [`mercedes-vous-remercie`](mercedes-vous-remercie/index.html) | Inchangé au premier commit | Aucun formulaire HTML détecté ; rôle à vérifier |
| [`mitsubishi-fuso`](mitsubishi-fuso/index.html) | Inchangé au premier commit | Capture équipée dans cette branche ; formId ADW-mitsubishi-fuso ; validation réelle requise |
| [`mitsubishi-fuso-remerciement`](mitsubishi-fuso-remerciement/index.html) | Inchangé au premier commit | Aucun formulaire HTML détecté ; rôle à vérifier |
| [`nettoyage-locaux-professionnels`](nettoyage-locaux-professionnels/index.html) | Inchangé au premier commit | Aucun formulaire HTML détecté ; rôle à vérifier |
| [`nissan-ariya`](nissan-ariya/index.html) | Modifié après premier commit | Capture équipée précédemment ; validation réelle requise |
| [`nissan-juke`](nissan-juke/index.html) | Modifié après premier commit | Capture équipée précédemment ; validation réelle requise |
| [`panneaux-photovoltaiques-energie-solaire`](panneaux-photovoltaiques-energie-solaire/index.html) | Modifié après premier commit | Capture équipée précédemment ; validation réelle requise |
| [`panneaux-photovoltaiques-panneaux-photovoltaique-valider`](panneaux-photovoltaiques-panneaux-photovoltaique-valider/index.html) | Inchangé au premier commit | Aucun formulaire HTML détecté ; rôle à vérifier |
| [`paritel`](paritel/index.html) | Inchangé au premier commit | Capture téléphone à adapter (1 formulaire(s)); GTM de référence installé, configuration à valider |
| [`paritel-typ`](paritel-typ/index.html) | Inchangé au premier commit | Aucun formulaire HTML détecté ; rôle à vérifier |
| [`paritel-vous-rembourse`](paritel-vous-rembourse/index.html) | Inchangé au premier commit | Capture téléphone à adapter (1 formulaire(s)); GTM de référence installé, configuration à valider |
| [`paritel-vous-rembourse-v2`](paritel-vous-rembourse-v2/index.html) | Inchangé au premier commit | Autre formulaire ou étape à qualifier : sans coordonnées détectées / à qualifier |
| [`politique-de-confidentialite-donnees-personnelles`](politique-de-confidentialite-donnees-personnelles/index.html) | Inchangé au premier commit | Aucun formulaire HTML détecté ; rôle à vérifier |
| [`primagaz`](primagaz/index.html) | Inchangé au premier commit | Capture équipée dans cette branche ; formId ADW-primagaz ; validation réelle requise |
| [`primagaz-obtenez-votre-gaz-propane-a-prix-fixe`](primagaz-obtenez-votre-gaz-propane-a-prix-fixe/index.html) | Inchangé au premier commit | Capture téléphone à adapter (1 formulaire(s)); GTM de référence installé, configuration à valider |
| [`primagaz-v2`](primagaz-v2/index.html) | Inchangé au premier commit | Autre formulaire ou étape à qualifier : sans coordonnées détectées / à qualifier |
| [`radius-remerciement`](radius-remerciement/index.html) | Inchangé au premier commit | Aucun formulaire HTML détecté ; rôle à vérifier |
| [`radius-telematics-typ`](radius-telematics-typ/index.html) | Inchangé au premier commit | Aucun formulaire HTML détecté ; rôle à vérifier |
| [`rc-pro-consultant-conseil-adw`](rc-pro-consultant-conseil-adw/index.html) | Inchangé au premier commit | Capture téléphone à adapter (1 formulaire(s)); GTM de référence installé, configuration à valider |
| [`remerciement-carte-cadeau`](remerciement-carte-cadeau/index.html) | Inchangé au premier commit | Autre formulaire ou étape à qualifier : sans coordonnées détectées / à qualifier |
| [`remerciement-panneaux-solaire`](remerciement-panneaux-solaire/index.html) | Inchangé au premier commit | Autre formulaire ou étape à qualifier : sans coordonnées détectées / à qualifier |
| [`remerciement-ticket-restaurant`](remerciement-ticket-restaurant/index.html) | Inchangé au premier commit | Autre formulaire ou étape à qualifier : sans coordonnées détectées / à qualifier |
| [`remerciement-ticket-restaurant-v2`](remerciement-ticket-restaurant-v2/index.html) | Inchangé au premier commit | Autre formulaire ou étape à qualifier : sans coordonnées détectées / à qualifier |
| [`remerciements-panneaux-solaires`](remerciements-panneaux-solaires/index.html) | Inchangé au premier commit | Autre formulaire ou étape à qualifier : sans coordonnées détectées / à qualifier |
| [`renault-capture`](renault-capture/index.html) | Inchangé au premier commit | Capture équipée dans cette branche ; formId ADW-renault-capture ; validation réelle requise |
| [`sage-gestion-de-la-paie-hd`](sage-gestion-de-la-paie-hd/index.html) | Inchangé au premier commit | Capture équipée dans cette branche ; formId ADW-sage-gestion-de-la-paie-hd ; validation réelle requise |
| [`sage-gestion-de-la-paie-hd-v4`](sage-gestion-de-la-paie-hd-v4/index.html) | Inchangé au premier commit | Autre formulaire ou étape à qualifier : sans coordonnées détectées / à qualifier |
| [`sauvie-defibrillateurs-en-entreprise`](sauvie-defibrillateurs-en-entreprise/index.html) | Inchangé au premier commit | Capture téléphone à adapter (1 formulaire(s)); GTM de référence installé, configuration à valider |
| [`securite-pro-v2`](securite-pro-v2/index.html) | Inchangé au premier commit | Autre formulaire ou étape à qualifier : sans coordonnées détectées / à qualifier |
| [`securite-professionnels`](securite-professionnels/index.html) | Modifié après premier commit | Capture équipée précédemment ; validation réelle requise |
| [`site`](site/index.html) | Inchangé au premier commit | Aucun formulaire HTML détecté ; rôle à vérifier |
| [`solutions-cles`](solutions-cles/index.html) | Inchangé au premier commit | Aucun formulaire HTML détecté ; rôle à vérifier |
| [`solutions-industrielles-cles-en-main`](solutions-industrielles-cles-en-main/index.html) | Inchangé au premier commit | Aucun formulaire HTML détecté ; rôle à vérifier |
| [`still-manutention`](still-manutention/index.html) | Modifié après premier commit | Capture équipée précédemment ; validation réelle requise |
| [`suivi-de-vehicules`](suivi-de-vehicules/index.html) | Modifié après premier commit | Capture équipée précédemment ; validation réelle requise |
| [`template-2`](template-2/index.html) | Inchangé au premier commit | Autre formulaire ou étape à qualifier : sans coordonnées détectées / à qualifier |
| [`ticket-restaurant`](ticket-restaurant/index.html) | Modifié après premier commit | Capture équipée précédemment ; validation réelle requise |
| [`ticket-restaurant-`](ticket-restaurant-/index.html) | Modifié après premier commit | Capture équipée précédemment ; validation réelle requise |
| [`ticket-restaurant-septembre`](ticket-restaurant-septembre/index.html) | Modifié après premier commit | Capture équipée précédemment ; validation réelle requise |
| [`ticket-restaurant-septembre-btp`](ticket-restaurant-septembre-btp/index.html) | Modifié après premier commit | Capture équipée précédemment ; validation réelle requise |
| [`ticket-restaurant-v2`](ticket-restaurant-v2/index.html) | Inchangé au premier commit | Autre formulaire ou étape à qualifier : sans coordonnées détectées / à qualifier |
| [`tns-prevoyance-v2`](tns-prevoyance-v2/index.html) | Modifié après premier commit | Capture équipée précédemment ; validation réelle requise |
| [`tns-prevoyance-v2-adw-test`](tns-prevoyance-v2-adw-test/index.html) | Modifié après premier commit | Capture équipée précédemment ; validation réelle requise |
| [`too-good-to-go`](too-good-to-go/index.html) | Modifié après premier commit | Capture équipée précédemment ; validation réelle requise |
| [`toyota-gamme-hybride`](toyota-gamme-hybride/index.html) | Inchangé au premier commit | Capture téléphone à adapter (1 formulaire(s)); GTM de référence installé, configuration à valider |
| [`typ-categ`](typ-categ/index.html) | Inchangé au premier commit | Aucun formulaire HTML détecté ; rôle à vérifier |
| [`typ-categories`](typ-categories/index.html) | Inchangé au premier commit | Iframe à examiner : ../typ-formulaires-vehicules-thank-you-page/, ../typ-formulaires-securite-thank-you-page/, ../typ-formulaires-energie-thank-you-page/, ../typ-formulaires-panneaux-thank-you-page/, ../typ-formulaires-caisses-thank-you-page/, ../typ-formulaires-typ-log-entreprise/ |
| [`typ-energie`](typ-energie/index.html) | Inchangé au premier commit | Autre formulaire ou étape à qualifier : sans coordonnées détectées / à qualifier |
| [`typ-formulaires-caisses-thank-you-page`](typ-formulaires-caisses-thank-you-page/index.html) | Inchangé au premier commit | Autre formulaire ou étape à qualifier : sans coordonnées détectées / à qualifier |
| [`typ-formulaires-energie-thank-you-page`](typ-formulaires-energie-thank-you-page/index.html) | Inchangé au premier commit | Autre formulaire ou étape à qualifier : sans coordonnées détectées / à qualifier |
| [`typ-formulaires-form-typ-vehicules`](typ-formulaires-form-typ-vehicules/index.html) | Modifié après premier commit | Capture équipée précédemment ; validation réelle requise |
| [`typ-formulaires-panneaux-photovoltaiques`](typ-formulaires-panneaux-photovoltaiques/index.html) | Inchangé au premier commit | Autre formulaire ou étape à qualifier : sans coordonnées détectées / à qualifier |
| [`typ-formulaires-panneaux-thank-you-page`](typ-formulaires-panneaux-thank-you-page/index.html) | Inchangé au premier commit | Autre formulaire ou étape à qualifier : sans coordonnées détectées / à qualifier |
| [`typ-formulaires-securite-thank-you-page`](typ-formulaires-securite-thank-you-page/index.html) | Inchangé au premier commit | Autre formulaire ou étape à qualifier : sans coordonnées détectées / à qualifier |
| [`typ-formulaires-typ-caisses-enregistreuse`](typ-formulaires-typ-caisses-enregistreuse/index.html) | Modifié après premier commit | Capture équipée précédemment ; validation réelle requise |
| [`typ-formulaires-typ-energie-form`](typ-formulaires-typ-energie-form/index.html) | Modifié après premier commit | Capture équipée précédemment ; validation réelle requise |
| [`typ-formulaires-typ-log-entreprise`](typ-formulaires-typ-log-entreprise/index.html) | Inchangé au premier commit | Autre formulaire ou étape à qualifier : sans coordonnées détectées / à qualifier |
| [`typ-formulaires-typ-panneaux-form`](typ-formulaires-typ-panneaux-form/index.html) | Modifié après premier commit | Capture équipée précédemment ; validation réelle requise |
| [`typ-formulaires-typ-secu-form`](typ-formulaires-typ-secu-form/index.html) | Inchangé au premier commit | Capture téléphone à adapter (1 formulaire(s)); GTM de référence installé, configuration à valider |
| [`typ-formulaires-vehicules-thank-you-page`](typ-formulaires-vehicules-thank-you-page/index.html) | Inchangé au premier commit | Autre formulaire ou étape à qualifier : sans coordonnées détectées / à qualifier |
| [`typ-ticket-restaurant`](typ-ticket-restaurant/index.html) | Inchangé au premier commit | Autre formulaire ou étape à qualifier : sans coordonnées détectées / à qualifier |
| [`une-rentree-sous-le-signe-du-pouvoir-d-achat`](une-rentree-sous-le-signe-du-pouvoir-d-achat/index.html) | Modifié après premier commit | Capture équipée précédemment ; validation réelle requise |
| [`vehicules-de-societe-hd`](vehicules-de-societe-hd/index.html) | Modifié après premier commit | Capture équipée précédemment ; validation réelle requise |
| [`vehicules-professionnel-v2`](vehicules-professionnel-v2/index.html) | Inchangé au premier commit | Autre formulaire ou étape à qualifier : sans coordonnées détectées / à qualifier |
| [`vehicules-utilitaires`](vehicules-utilitaires/index.html) | Ajouté après premier commit | Capture équipée précédemment ; validation réelle requise |
| [`voiture-nouveau-range-rover`](voiture-nouveau-range-rover/index.html) | Inchangé au premier commit | Capture téléphone à adapter (2 formulaire(s)); GTM de référence installé, configuration à valider |
| [`voiture-range-rover`](voiture-range-rover/index.html) | Inchangé au premier commit | Capture téléphone à adapter (1 formulaire(s)); GTM de référence installé, configuration à valider |
| [`volvo`](volvo/index.html) | Inchangé au premier commit | Capture téléphone à adapter (2 formulaire(s)); GTM de référence installé, configuration à valider |
