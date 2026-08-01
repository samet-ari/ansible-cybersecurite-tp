# Ansible – Cybersécurité et Automatisation

## Contexte

Ce projet a été réalisé dans le cadre d'un TP à La Plateforme_ (Marseille).
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
- Secrets gérés via Ansible Vault (`inventory/group_vars/all/vault.yml`)

## Structure du dépôt
## Prérequis

- Ansible >= 2.19
- Collections : `community.general`, `ansible.posix`
- Accès SSH par clé aux machines cibles
- Python 3 installé sur les cibles

## Utilisation

```bash
ansible all -m ping --ask-vault-pass
ansible-playbook playbooks/site.yml --ask-vault-pass
```

## Avancement

- [x] Job 1 – Prise en main et premières automatisations
- [x] Job 2 – Hardening des systèmes (utilisateurs, SSH, UFW, services)
- [x] Job 3 – Surveillance, logs et conformité (Filebeat, audit, sysctl/PAM, rôle Ansible)
- [ ] Job 4 – Détection, réponse à incident
- [ ] Job 5 – Scénario final et bilan

## Notes

Voir `docs/notes_techniques.md` pour le détail des limitations rencontrées
dans l'environnement de conteneurs Docker (absence de systemd, capabilities
réseau) et les solutions mises en œuvre.
