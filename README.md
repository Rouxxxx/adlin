# ADLIN-Projet-ANSIBLE

## Dependances
- gueerlingguy.apache
- gueerlingguy.certbot
- happydns.happydomain

## Liste des playbooks

### basis.yml
Premier playbook a être exécuté sur une nouvelle machine. Se connecte en SSH en tant que root pour effectuer différentes actions :
- mettre la machine à jour
- installer sudo
- créer le groupe ssh_group (si il n'existe pas)
- créer un user **paul.leroux**, avec les permissions sudo et dans le groupe ssh_group
- permettre aux users de sudo sans passwd

### vitrine.yml

Permet de créer le premier site vitrine. Il va :
- installer apache et certbot
- copier le site en hugo si besoin
- enable apache au démarrage
- enable le premier site dans apache
- copier la configuration du premier site
- créer les certificats du premier site


### name-server.yml

Permet de créer le second site vitrine. Il va :
- installer apache, knot et certbot
- copier le site en hugo si besoin
- copier les fichiers de configuration de knot (config de knot + de la zone paul.leroux.srs.drivee.site)
- configurer happydomain, avec la creation d'un sous-domaine 'my_cool_subdomain'
- enable knot et apache au démarrage
- enable le second site dans apache
- copier la configuration du second site
- créer les certificats du second site
- mettre la regénération des certificats dans la crontab

### securing.yml

Permet de sécuriser la machine en prévision de futures attaques. Il va :
- sécuriser les différents paramètres de connexion SSH
- installer et configurer fail2ban
- mettre en place le pare-feu de la machine avec nftables