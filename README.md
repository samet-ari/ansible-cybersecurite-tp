# Ansible – Cybersécurité et Automatisation

## Contexte

Ce projet a été réalisé dans le cadre d'un TP à La Plateforme_.
Le scénario : au sein d'une entreprise fictive nommée **Starfleet**, une équipe
d'administrateurs système et sécurité utilise Ansible pour automatiser le
durcissement (hardening), la supervision et la réponse à incident sur une
infrastructure Linux hétérogène (Debian et Rocky Linux).

## Environnement de TP

- **Nœud de contrôle** : Debian (WSL2)
- **Machines cibles** : 3 conteneurs Docker
  - `web1`, `web2` : Debian 12 (groupe `webservers`)
  - `db1` : Rocky Linux 9 (groupe `dbservers`)
- Connexion SSH par clé (sans mot de passe), réseau Docker dédié `ansible-net`

## Structure du dépôt
## Prérequis

- Ansible >= 2.19
- Accès SSH par clé aux machines cibles
- Python 3 installé sur les cibles

## Utilisation

```bash
ansible all -i inventory/inventory.ini -m ping
ansible-playbook -i inventory/inventory.ini playbooks/check_services.yml
```

## Avancement

- [x] Job 1 – Prise en main et premières automatisations
- [ ] Job 2 – Hardening des systèmes
- [ ] Job 3 – Surveillance, logs et conformité
- [ ] Job 4 – Détection, réponse à incident
- [ ] Job 5 – Scénario final et bilan
