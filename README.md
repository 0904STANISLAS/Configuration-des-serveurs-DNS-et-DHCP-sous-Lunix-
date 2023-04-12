# Nom-Projet

Pour installer  le serveur DNS on tape la commande :
sudo  apt-get install  bind9

Une fois le serveur installer nous devons recuperer le nom de  l'host en faisant:
nano /etc/hostname   

Verifier si le serveur a une adresse IP en faisant:
ifconfig 

S'il ne dispose pas d'adresse IP, créez en, en faisant:
ifconfig enp0s3 (adresse IP à créer)

Vous pouvez vérifier si l'adresse a été créer en faisant:
ifconfig

On  doit vérifier le fichier de résolution qui nous donnes le nom du domaine de l'adresse IP en faisant:
nano /etc/resolv.conf

Une fois le nom du domaine vérifier on se place dans le fichier racine pour configurer notre DNS en faisant:
cd /etc/bind

On doit créer le fichier de configuration DNS en faisant:
nano named.conf.local

On fait la copie du fichier en faisant:
cp db.local direct 

Pour voir le fichier copier on fait:
nano direct

On modifie le nom de la machine, du domaine et l'adresse IP

on copie ensuite le fichier direct en faisant :
cp direct inverse 

dans le fichier on vas jjuste remplacer le nom du domaine par le nom de la machine.

On vérifie s'il y a pas d'erreur en faisant :
named-checkconf -z

S'il y a pas d'erreur on redemare le systeme en faisant:
systemctl restart bind9

Une fois le système rédemarer on peut allumer le serveur en faisant:
systemctl status bind9

Pour installer le serveur DHCP on fait:
apt install isc-dhcp-server
N.B : on doit s'assurer au niveau de la configuration nous devons etre sur NAT

On peut maintenant changer le mode d'acces en se connectant au reseau local

On doit changer d'interface en faisant: 
nano /etc/default/isc-dhcp-server

Accedons au fichier de configuration an faisant :
nano /etc/dhcp/dhcp.conf

Ajoutons les informations essentielles pour le paramétrage du serveur:
l'adresse IP, le masque de sous-reseau, nom du domaine(identique au serveur DNS), adresse du routeur

Verifions s'il existe une adresse IP :
ifconfig

S'il n'existe pas on doit créer en faisant:
ifconfig enp0s3 (adresse ip)

On peut vérifier si l'adresse IP est créée en faisant:
ifconfig

On peut verifier si la configuratuion n'a pas d'erreur en faisant:
dhcpd -t

S'il y a pas d'erreur on peut rédemarer le systeme en faisant:
systemctl restart isc-dhcp-server
On oublie pas le fichier de resolution pour fixer l'adresse du serveur et le nom du domaine en faisant :
nano /etc/reslov.conf

et on peut maintenant redemarer. 

On peut demarer le serveur DHCP :
system restart isc-dhcp-server
status isc-dhcp-server

On peut aussi demarer le serveur DNS en faisant:
systemctl restargt bind9
systemctl status bind9


