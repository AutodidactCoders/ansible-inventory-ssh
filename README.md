# Ansible - Static inventory

Comment créer et utiliser un inventaire statique Ansible ?

1. Prérequis

- Une machine d'administration avec Ansible (voir https://github.com/AutodidactCoders/ansible-hello-world) Ici, elle porte l'IP 192.168.0.13
- Une machine avec Python préinstallé et un accès SSH vers celle-ci. Ici, cette machine est virtuelle, elle a la configuration réseau suivante :
![alt text][network_config]

[network_config]: https://github.com/AutodidactCoders/ansible-static-inventory/blob/master/ubuntu-demo-node-1_ip-addresses.png "ubuntu-demo-node-1 network"

2. Premier inventaire

Ce type d’inventaire est écrit à la main et non généré par un outil comme peut l’être l’inventaire dynamique.

Un inventaire liste des informations sur les machines qui seront nécessaires à Ansible pour s’y connecter, récupérer des  informations, et si besoin les configurer. 

Voici un exemple d’inventaire (le plus basique) : 
```
ubuntu-demo-node-1
```
Avec l'ajout de détails concernant la connexion SSH vers cette machine, le fichier devient :

- Si l’authentification SSH se fait via mot de passe
```
ubuntu-demo-node-1 ansible_ssh_host=192.168.0.101 ansible_ssh_user=ubuntu ansible_ssh_pass=MotDePasse
```
- Si l’authentification SSH se fait via clé privée
```
ubuntu-demo-node-1 ansible_ssh_host=192.168.0.101 ansible_ssh_user=ubuntu ansible_ssh_private_key_file=/home/bme/.ssh/id_rsa
```
Un autre élément important de l'inventaire est la déclaration de groupe. Ce qui permet de jouer un playbook sur un ensemble de machines en spécifiant le nom du groupe dans le playbook.

3. Utilisation de l'inventaire

Le playbook affiche un "Hello world" dans la console suivie du hostname ainsi que de l'IP dite "par défaut" (c'est la première IP de la liste qu'Ansible a récupérée lors de la phase "Ghatering Facts") de la machine concernée par le script.

- Pour jouer le playbook sur un noeud spécifique :

```shell
ansible-playbook hello_world_node.yml -i inventory 
```

![alt text][hello_world_node]

[hello_world_node]: https://github.com/AutodidactCoders/ansible-static-inventory/blob/master/hello_world_node.png "Hello World Node"

- Pour jouer le playbook sur un groupe de noeuds :

```shell
ansible-playbook hello_world_group.yml -i inventory 
```

![alt text][hello_world_group]

[hello_world_group]: https://github.com/AutodidactCoders/ansible-static-inventory/blob/master/hello_world_group.png "Hello World Group"

A très vite sur https://blog.autodidactcoders.com

