# Backup and Restore Guide

This document describes the backup and restore procedures for the IAM project, including **Keycloak** and **Postgres**.  
All backups should be stored outside of the running containers (e.g. in `backups/` or an external volume).

---

## 1. Keycloak

### Export (Backup)
Export the full Keycloak configuration (realms, clients, roles, users) from the running container:

```bash
docker exec -it keycloak /opt/keycloak/bin/kc.sh export --dir /opt/keycloak/data/export
```

The exported files will be available in the container at `/opt/keycloak/data/export`.
Mount this path to a persistent host directory (e.g. `./backups/keycloak/`) to keep backups safe.

### Import (Restore)

Restore a Keycloak configuration from an export:

```bash
docker exec -it keycloak /opt/keycloak/bin/kc.sh import --dir /opt/keycloak/data/export
```

> ⚠️ Import will overwrite existing realms and clients. Test imports in a staging environment before running in production.

---

## 2. Postgres

### Backup (Dump)

Create a database dump using `pg_dump`:

```bash
docker exec -t postgres pg_dump -U "$POSTGRES_USER" "$POSTGRES_DB" > backups/postgres/iam-$(date +%F).sql
```

* Replace `${POSTGRES_USER}` and `${POSTGRES_DB}` with the values from your `.env`.
* The dump file will be saved on the host in `backups/postgres/`.

### Restore (Load)

Restore a database dump into Postgres:

```bash
cat backups/postgres/iam-YYYY-MM-DD.sql | docker exec -i postgres psql -U ${POSTGRES_USER} -d ${POSTGRES_DB}
```

Replace `iam-YYYY-MM-DD.sql` with the filename of the backup you want to restore.

---

## 3. Best Practices

* **Automate backups**: Use cron jobs or systemd timers to run these commands daily.
* **Keep secrets safe**: Database passwords and Keycloak admin credentials must not be committed to Git. Store them in `.env.secret`.
* **Verify restores**: Regularly test restoring backups in a staging environment.
* **Retention**: Keep at least 7 daily backups and 3 monthly snapshots.
* **Offsite storage**: Sync `backups/` to cloud storage or external drives for disaster recovery.

---

## 4. References

* [Keycloak Export/Import](https://www.keycloak.org/server/importExport)
* [Postgres Backup Documentation](https://www.postgresql.org/docs/current/backup.html)

---

