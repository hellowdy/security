
Sommaire:

- [Proposition de sécurisation d'une application](#proposition-de-sécurisation-dune-application)
    - [Introduction :](#introduction-)
      - [Que veut dire sécuriser un système ?](#que-veut-dire-sécuriser-un-système-)
      - [Contre quoi doit-on se sécuriser ?](#contre-quoi-doit-on-se-sécuriser-)
      - [Comment sécuriser un système ?](#comment-sécuriser-un-système-)
    - [Les stratégies générales de la sécurisation :](#les-stratégies-générales-de-la-sécurisation-)
    - [Les protocoles de protection de l'échange de données](#les-protocoles-de-protection-de-léchange-de-données)
      - [Hachage, salage](#hachage-salage)
      - [Protection du navigateur](#protection-du-navigateur)
      - [Politique des mots de passes](#politique-des-mots-de-passes)
      - [La sanitisation](#la-sanitisation)
      - [Quelle est la différence entre Authentification et Autorisation ?](#quelle-est-la-différence-entre-authentification-et-autorisation-)
      - [L’accès aux données](#laccès-aux-données)
      - [Token](#token)
      - [La session](#la-session)
      - [La sécurisation de l'API](#la-sécurisation-de-lapi)
      - [La journalisation](#la-journalisation)
      - [La stratégie de sauvegarde de serveur](#la-stratégie-de-sauvegarde-de-serveur)
      - [Dernière étapes de l'application](#dernière-étapes-de-lapplication)
      - [Sources](#sources)

# Proposition de sécurisation d'une application
### Introduction :
In documentation, we go speak the security the application. We go have how  do and why ?
Firstly, we will see how to secur a system with three keys words :
- Confidentiality
- Intégrity
- Avialability 

Later, we will speak the existing threats with : XSS, DDOS, SQLI...
Next, we will talk how fall into place  step-by-step the securiting

#### Que veut dire sécuriser un système ?
De nos jours, chaque entreprise utilise un réseau, et la cybersécurité devient urgente car les cybercriminels attaquent les réseaux des entreprises à la recherche de données confidentielles. Il est donc vital d'installer une protection pour protéger ces données. 
Selon la *RGPD* des mesures dites « d’  hygiène » constituent un socle permettant de protéger la plupart des systèmes :
- __La confidentialité__ : Nous ne donnerons pas accès aux ressources à des personnes non autorisées, seuleument en fonction du "grade" de la personne pour utiliser certaines ressources sur l'ordinateur.   
Pareillement pour l'accès dans les locaux, et à certains étages. 
De plus, afin de protéger les données sensibles, nous conseillerons de les chiffrer pour que les hackers aient des difficultés à déchiffrer.
- __L'intégrité__ : Nous veillerons à ce que le message transmit entre deux personnes ne soit pas lu et/ou modifié par une personne extérieure. 
- __La disponibilité__: Nous veillerons à ce que les ressources n'aient pas disparu et que les bonnes données reste attribué au bon utilisateur.

La __RGPD (Règlement Général sur la Protection des Données)__ est un texte réglementaire européen qui encadre le traitement des données de manière égalitaire sur tout le territoire de l’Union Européenne. Les personnes extérieurs à l'Union Européennes doivent appliquer la réglementation, lors d'un échange avec des personnes issues de l'UE.

#### Contre quoi doit-on se sécuriser ? 
La cyberattaque utilise différents types d'attaques que nous allons évoquer:

__Le vol de données__ est équivalent au vol de l'information. Cela peut être de nature confidentielle, personnelle ou financière. A l'aide de ces informations, une personne malveillante peut par exemple usurper une identité.

__La compromission des ressources__ est une violation de l'intégralité du contenu permettant à l'attaquant de le modifier. 
*L'attaque par "point d'eau" (whatering hole attack)*, fait référence à la stratégie du prédateur attendant sa proie à un point d'eau. 
Une personne malveillante tendra alors un piège au visiteur en modifiant le contenu légitime du site afin de récupérer ses données sensibles.

__XSS (Cross-site scripting)__ est une faille de sécurité qui permet à l'attaquant d'injecter dans un site web un code client malveillant. Dès que la victime utilise ce code à son insu, l'attaquant esquive le contrôle d'accès et s'approprie l'identité de l'utilisateur.

__CSRF (Cross-Site Request Forgery)__ Une personne malveillante va prendre le contrôle d'une session déjà autorisée par un utilisateur afin d'envoyer des données non désirées vers un autre site web. 
Le plus courant dans une attaque CSRF sont le vol de données, d'identité ou d'argent.

__SQLI (Structured Query Language Injection)__ Comme son nom l'indique, il injecte des éléments dans le code SQL afin de manipuler des données importantes, notamment à partir d'un formulaire.

__DDOS (Distributed Denial of Service)__ Une attaque nommé *déni de service*, permet à un hacker de faire "sauter" un serveur en envoyant plusieurs requêtes, le site sera indisponible pour les utilisateurs.

#### Comment sécuriser un système ?
La stratégie générale de la sécurisation se résume en trois points que nous allons détailler : 
    - Défense en profondeur
    - Moindre privilège 
    - Réduction de la surface d'attaque

__La défense en profondeur__ est basée sur plusieurs couches sécurisées permettant lors d'une attaque, d'isoler la couche attaquée, afin de pouvoir contrer la menace.
Une mauvaise pratique serait de négliger la sécurisation, en se focalisant sur une seule couche en délaissant les autres.
__Le moindre privilège__ consite à limiter l'accès aux ressources, à certaines personnes concernés, lors d'un projet commun.
Si une personne travaille en collaboration avec votre projet et a besoin d'avoir accès à certaines données spécifiques, vous lui fournirez juste les données dont elle à besoin sans lui donner accès aux autres.
__Réduction de la surface d'attaque__ signifie que notre système d'information est exposé et susceptible d'être attaqué. Le problème est que plus la surface est grande, plus l'étendue du problème sera important. Pour pallier à cette difficulté, nous diminuerons la surface afin de concentrer l'attaque sur un point. Ce qui facilitera la mise en place de la sécurité

### Les stratégies générales de la sécurisation :
### Les protocoles de protection de l'échange de données
L'application que nous allons concevoir va être sur plusieurs navigateurs. Pour commencer, nous allons évoquer le système __HTTP (Hyper Text Transfer Protocol)__, qui est un protocole de transfert d'information permettant d'échanger entre le client et le serveur.

Le problème est que *HTTP*, n'étant pas encore sécurisé, est susceptible de se faire attaquer par le "man-in-the-middle". Cette troisième personne est un hacker, pouvant intercepter le contenu d'un message ou d'une information, le lire et/ou le modifier avant de le renvoyer au vrai destinataire.

Pour sécuriser la liaison, nous allons mettre en place le __TLS (Transport Layer Security)__  permettant de chiffrer le contenu devenant ainsi difficile à lire.
Alors, *HTTP* avec la sécurisation *TLS* devient *HTTPS*.

__HSTS (HTTP Strict Transport Security)__ permet de verrouiller la sécurité en redirigeant le site HTTP vers un HTTPS. Cependant, cela ne marche pas lors de la première visitation sur un site. 

#### Hachage, salage 
Pour plus de sécurité, nous proposons, lorsque nous devons manipuler des données sensibles tels que des mots de passe, préférer ne pas les utiliser en "clair" mais les chiffrer avec une fonction de hachage.
Le hachage fonctionne notamment avec un algorithme nommé *SHA-256*, permettant d'obtenir une empreinte unique du fichier chiffré. Ce dernier respecte la *RGPD* et il est sécurisant. Il est ainsi impossible de revenir en arrière pour avoir le message initial sauf si on a retrouvé la clé correspondante.

Pour palier à ce problème, nous rajouterons une sécurisation supplémentaire au hachage appelé salage. 
Le salage consiste à ajouter "du sel" (un mot) connu seulement de l'utilisateur, et de l'ajouter à l'empreinte du hachage.
L'ensemble doit être mixé à nouveau avec le hachage afin d'obtenir un message chiffré différent. Cette fois-ci, il sera plus difficile de le déchiffrer car il faut connaître  "le sel".

#### Protection du navigateur
Notre application va être utilisée sur internet, c'est pourquoi nous devons sécuriser les navigateurs.

La première protection du navigateur, par défaut est la __SOP (Same-Origin Policy)__.
La sécurité de la *SOP* permet à deux sites différents de ne pas s'échanger des informations. 

La deuxième protection est le __CORS(Cross-origin resource sharing)__. Ce dernier permet de contourner la *SOP* et d'autoriser certains sites différents à échanger des informations.

La troisième proctection est le __CSP(Constent Secure Policy)__ sécurise davantage après avoir autorisé la *CORS*. Le *CSP* fonctionne avec une 'liste blanche', autorisant seulement ce qu'il y a sur cette liste et interdisant le reste.

La dernière est le __SRI(Subresource Integrity)__ permet d'analyser si l'intégrité du contenu d'une sous-ressource extérieur au site n'a pas été modifié et ne contient pas de faille.
Pour vérifier que le *SRI* n'a pas été modifié, le navigateur doit constater qu'il n'y a pas eu manipulation. Cela fonctionne avec un hachage qui doit correspondre avec le fichier récupéré.

#### Politique des mots de passes
Notre politique des mots de passe fonctionne avec certains paramètres :
- Le mot de passe doit être chiffré dans la base de données.
- La longueur du mot de passe doit être long, car plus il sera long plus cela sera difficile à hacker.
- La demande d'authentification doit être demandée avant une manipulation sensible 
- Un délai d'expiration du mot de passe pour les modérateurs et administrateurs au sein d'un site doit être mis en place pour une durée de quatre mois.
- La méthode de conservation dans un coffre fort permet de garder un mot de passe unique pour l'ouvrir,et contenir une multitude de mots de passe.
- Limitation d'une tentative ratée pour s'authentifier.

#### La sanitisation
la sanitisation permet de nettoyer les données reçues d'un utilisateur avant de l'envoyer dans la base de données. Toute demande passe par un formulaire. On doit vérifier si le formulaire ne contient rien de dangereux pour notre application :
Depuis le front (visibilité sur l'écran): limiter les caractères, obliger à mettre que des numéros ou que des lettres...
Depuis le back : vérifier l'existence d'une faille comme SQLI.. 

#### Quelle est la différence entre Authentification et Autorisation ?
L'authentification est la vérification de l'identité de la personne souhaitant entrer dans l'application.
Après la vérification,  si la personne est autorisé à entrer, elle pourra utiliser les ressources disponible pour lui.

#### L’accès aux données
Pour sécuriser le réseau de l'application, nous allons mettre en place la règle du moindre privilège en appliquant le R-BAC (Role Based Access Control). Cela signifie que chaque personne aura accès à certaines ressources en fonction du rôle occupé au sein de l'entreprise. Il existe différents rôles :
- Administrateur 
- Modérateur 
- Rédacteur 
- Utilisateur 

#### Token
Nous proposons des jetons d'authentification à double facteur qui mettent en place une sécurisation, permettant lors de l'ouverture d'une session, d'obtenir un jeton confirmant ainsi son identité. Cela limitera les risques d'usurpation.

Afin de garder la session de l'utilisateur sécurisé, nous allons prendre des dispositions avec le jeton :
- la durée du jeton délivré ne doit pas excéder quelques minutes lors de la création de sa session en validant par mail ou par sms.
- Les jetons ne doivent pas permettre à l'utilisateur de s'authentifier automatiquement afin d'accéder à sa session.

#### La session
Une fois authentifié avec succès, l'utilisateur aura accès à sa session suivant la règle du R-BAC, à savoir le moindre privilège. 
Pour sécuriser une session ouverte, nous proposons de limiter sa durée à une journée.
De plus, un cookie HTTP (cookie de navigateur) contient des données du serveur et les envoie vers le navigateur de l'utilisateur. Les cookies conservent des informations sur l'utilisateur (personnalisation, suivi..). Nous exclurons les données sensibles de l'utilisateur dans le cookie afin d'éviter lors d'une attaque, que l'attaquant usurpe l'identité de l'utilisateur.

#### La sécurisation de l'API
L'API (Application Programming Interface) permet d'accéder à la base de données de notre application, montrant les données, voire les données sensibles. Afin d'éviter les attaques de type SQLI, WSS ou MITM, nous devons sécuriser notre API.
Pour la sécuriser, nous avons mis en place HTTPS et les jetons d'identification. 
De plus, nous recommandons de mettre en place :
- Limiter et anticiper les requêtes lors d'une attaque DDOS.
- Nous conseillons l'utilisation d'une API Stateless permettant de récupérer des informations précises. De plus, il ne garde aucune trace de ces échanges précédents, Permettant ainsi de sécuriser davantage.

#### La journalisation
Nous proposons la journalisation qui fonctionne comme un journal, permettant de garder une trace de chaque log effectué dans la journée. 

#### La stratégie de sauvegarde de serveur
Pour plus de sécurisation, nous conseillons de mettre en place une stratégie de sauvegarde de serveur chaque jour à minuit par deux entreprises différentes. Permettant ainsi de conserver un historique de la journée. 
De ce fait, si nous rencontrons un problème, il suffit de reprendre une des deux sauvegardes pour récupérer toute les données.

#### Dernière étapes de l'application
Lorsque notre application sera sortie, nous proposerons de réaliser un audit PASSI afin de tester la sécurité de notre application. 
Nous pourons éventuellement faire un bug bounty, faisant appel à des hackers professionnels dont le métier est de tester la sécurité de notre application contre une récompense. 

#### Sources
- https://www.vaadata.com/blog/fr/duree-validite-certificats-https/
- https://www.vaadata.com/blog/fr/rgpd-mesures-techniques-securite/
- https://stackoverflow.com/questions/6556522/authentication-versus-authorization
- https://www.ssi.gouv.fr/uploads/2013/05/anssi-guide-recommandations_mise_en_oeuvre_site_web_maitriser_standards_securite_cote_navigateur-v2.0.pdf
- https://www.ssi.gouv.fr/uploads/2021/10/anssi-guide-authentification_multifacteur_et_mots_de_passe.pdf