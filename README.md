# Présentation d'Ansible :

Ansible est une solution permettant de réaliser des déploiements, l’exécution de tâches et la gestion de configuration sur plusieurs machines 
en même temps. Il est agent-less et utilise SSH pour mettre en place les actions à réaliser, elles-mêmes écrites en YAML.

# Qu'est-ce qu'un playbook : 

Un playbook est un script qui s'applique sur tous les hosts renseignés dans les fichiers de configurations de "Ansible".
La configuration d'un playbook se fait selon le système d'exploitation des serveurs car celui-ci est écrit en ligne de commande.

# Fichier hosts.yaml :

Pour ajouter un serveur à la liste des playbook qui vont s'appliquer, il suffit de le rajouter dans le fichier généralement stockées dans 
etc/ansible/hosts (on ajoute directement les adresses ip de nos serveurs)
Dans notre cas, nous avons crée un nouveau fichier yaml : /home/user/playbooks/hosts.yml

# Commande d'utilisation des playbooks : 

ansible-playbook -i hosts.yaml -u root X
* Où X correspond au playbook à lancer sur les hosts.

# Gestion des Variables :

Avec Ansible, Les variables dans les playbooks sont très similaires à l'utilisation de variables dans n'importe quel langage de programmation. 
Il vous aide à utiliser et à affecter une valeur à une variable et à l'utiliser n'importe où dans le playbook. On peut mettre des conditions 
autour de la valeur des variables et les utiliser en conséquence dans le playbook.
Nous pourions crées un fichier où seront stockées toutes nos variables.
La façon la plus simple de définir des variables est de les insérer directement dans votre playbook à l’intérieur d’une section vars.

- hosts : <your hosts> 
- vars:
- tomcat_port : 8080 
  
# Ansible Vault :

Ansible Vault peut crypter tout fichier de données structuré utilisé par Ansible.
Le chiffrement par défaut est AES (qui est basé sur un secret partagé).

Création d'un vault:

$ mkdir -p group_vars/all
$ ansible-vault --ask-vault-pass create group_vars/all/vault

On y met une variable contenant notre mot de passe:

vault_utux_passwd: "{{ 'secret' | password_hash('sha256') }}"

Et si on veut l'éditer:

$ ansible-vault --ask-vault-pass edit group_vars/all/vault

On exécute notre playbook:

ansible-playbook myuser.yml --ask-vault-pass

Ça marche, mais c'est un peu lourd car il faut taper le mot de passe vault à chaque exécution du playbook. Heureusement on peut le définir dans un fichier. On prendra soin de faire un gitignore pour ce fichier, voire même le placer dans un autre dossier:

$ echo "motdepassevault" > vault_passwd
$ echo "vault_passwd" >> .gitignore

On doit ensuite spécifier à Ansible où trouver ce fichier. Vous pouvez le définir au niveau du /etc/ansible/ansible.cfg ou dans le ansible.cfg local du projet (ce que je préfère faire, ainsi il est commité dans le dépôt et tout le monde a la bonne version):

#ansible.cfg
[defaults]
vault_password_file = vault_passwd

Vous devriez maintenant pouvoir exécuter votre playbook sans le --ask-vault-pass.

Hakim AZOUR & Jordan WAGNER
