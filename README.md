ansible-maint-backup-mysql-es
=============================

This ansible role can be used to back up the MySQL databases and the Elasticsearch indices of the target host:

- MySQL backups are produced with mysqldump (some databases are excluded), and compressed with gzip.
- To back up Elasticsearch indices, a snapshot repository is configured in the Elasticsearch server, and a snapshot of all indices is taken, then a tarball file (.tgz) of the repository is made
- Backups are stored in the directory `{{ maint_backup_basepath }}/current/` (default value: `/var/artefactual/maint-backups/current`) (If there is a previous backup in the `current` directory, the old `current` directory is renamed before storing the new backups)

Use the companion role [`ansible-maint-restore-mysql-es`](https://github.com/artefactual-labs/ansible-maint-restore-mysql-es) to restore the databases and indices from the backups.


Role Variables
--------------

Refer to [defaults/main.yml](defaults/main.yml)


Example Playbook
----------------

```yaml
- name: "Take backups of mysql/ES"
  hosts:
    - targethost
  become: yes
  tasks:
    - import_role: 
        name: "maint-backup-mysql-es"
      tags: maint-backup-mysql-es
```


Restore the databases and indices to a different host
--------------------------------------------------

It is possible to use this role and the companion role `ansible-maint-restore-mysql-es` to copy the databases/indices to another
host. For more information, please see the [README for the companion role  `ansible-maint-restore-mysql-es`](https://github.com/artefactual-labs/ansible-maint-restore-mysql-es)


License
-------

BSD

Author Information
------------------

Artefactual Systems
