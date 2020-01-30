# Qu'est-ce qu'un playbook : 

Un playbook est un script qui s'applique sur tous les hosts renseignés dans les fichiers de configurations de "Ansible".
La configuration d'un playbook se fait selon le système d'exploitation des serveurs car celui-ci est écrit en ligne de commande.

# Commande d'utilisation des playbooks : 

ansible-playbook -i hosts.yaml -u root Y

Où Y correspond au playbook à lancer sur les hosts.

# Fichier hosts.yaml :

Correspond aux adresses IP des serveurs (/home/user/playbooks/hosts.yml)
Pour ajouter un serveur à la liste des playbook qui vont s'appliquer, il suffit de le rajouter dans ce fichier


Hakim AZOUR & Jordan WAGNER
