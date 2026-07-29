# Notes techniques - Défis rencontrés

## Environnement de conteneurs Docker (limitation systemd)

Les machines cibles de ce TP sont des conteneurs Docker (`debian-target`,
`rocky-target`) dans lesquels `sshd` s'exécute directement en PID 1, sans
systemd comme init system. Cela a eu deux conséquences :

1. **Redémarrage de service** : le module `service`/`systemd` ne peut pas
   redémarrer sshd de façon classique - un redémarrage tue le PID 1 et arrête
   le conteneur. Solution retenue : envoi d'un signal `SIGHUP` via
   `pkill -HUP -x sshd` pour recharger la configuration sans interrompre le
   service (voir `playbooks/harden_ssh.yml`).

2. **Désactivation des services inutiles (Job 2.4)** : le module
   `ansible.builtin.systemd` échoue avec l'erreur *"System has not been
   booted with systemd as init system (PID 1). Can't operate."* Le playbook
   `playbooks/disable_services.yml` reste néanmoins valide et fonctionnel :
   il est écrit pour un environnement de production standard (VM avec
   systemd), où `cups`, `avahi-daemon` et `bluetooth` seraient normalement
   présents et gérés par systemd. La gestion d'erreur (`ignore_errors: true`)
   permet au playbook de continuer proprement sans échec bloquant, même
   dans cet environnement contraint.

3. **Pare-feu UFW (Job 2.3)** : nécessite la capability Docker `NET_ADMIN`
   pour manipuler `iptables`/`nftables` à l'intérieur du conteneur. Les
   conteneurs ont été recréés avec `--cap-add=NET_ADMIN` pour permettre le
   bon fonctionnement du module `community.general.ufw`.

## Conclusion

Ces limitations sont spécifiques à l'environnement de lab (conteneurs) et
n'affecteraient pas un déploiement réel sur des machines virtuelles Linux
classiques avec systemd. Elles illustrent cependant l'importance de bien
connaître son environnement cible avant d'automatiser, et la nécessité de
prévoir une gestion d'erreur robuste dans les playbooks.
