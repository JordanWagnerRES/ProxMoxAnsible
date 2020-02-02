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


Hakim AZOUR & Jordan WAGNER
