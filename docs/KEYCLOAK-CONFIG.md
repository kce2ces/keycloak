
# Keycloak Configuration

This document describes the Keycloak setup used in the IAM configuration project.  
It includes realms, clients, user federation, roles, groups, integration notes, and backup/restore procedures.

---

## 1. Realm Setup
- **Realm Name:** `krp` (example, adjust as needed)
- **Description:** Identity and Access Management for IAM and connected services
- **Enabled:** Yes
- **Default Roles:** `user`

---

## 2. Clients

### Nextcloud
- **Client ID:** `nextcloud`
- **Protocol:** OpenID Connect
- **Redirect URIs:**
  - `https://nc.timebank.tw/*`
- **Web Origins:**
  - `https://nc.timebank.tw`
- **Secret:** stored in `.env.secret` (not in repo)

### OpenWebUI
- **Client ID:** `openwebui`
- **Protocol:** OpenID Connect
- **Redirect URIs:**
  - `https://ai.timebank.tw/oidc/callback`
- **Web Origins:**
  - `https://ai.timebank.tw`

### WordPress
- **Client ID:** `wordpress`
- **Protocol:** OpenID Connect
- **Redirect URIs:**
  - `https://wp.timebank.tw/*`

---

## 3. Identity Providers
(Optional, if federating with external providers)

### Google Identity Provider
- **Protocol:** OpenID Connect
- **Client ID/Secret:** stored in `.env.secret`

### LDAP Federation
- **Host:** `ldap://openldap.local`
- **Base DN:** `dc=timebank,dc=tw`
- **Bind Credentials:** stored in `.env.secret`

---

## 4. User Roles
- **Default roles:** `user`
- **Admin roles:** `realm-admin`, `app-admin`
- **Service-specific roles:**  
  - `nextcloud-admin`  
  - `openwebui-user`

---

## 5. Groups
- `staff`  
- `volunteers`  
- `developers`  

---

## 6. Integration Notes
- All secrets (client secrets, database passwords) are **not in Git**. They are stored in `.env.secret`.  
- When adding a new service:
  1. Create a Keycloak client.  
  2. Configure redirect URIs.  
  3. Add client secret to `.env.secret`.  
  4. Update the service’s OIDC config (Nextcloud, OpenWebUI, WordPress, etc.).  

---

## 7. Backup and Restore

### Export (Backup)
Keycloak configuration is exported using:
```bash
docker exec -it keycloak /opt/keycloak/bin/kc.sh export --dir /opt/keycloak/data/export
```

### Import (Restore)
Keycloak configuration is restored using:
```bash
docker exec -it keycloak /opt/keycloak/bin/kc.sh import --dir /opt/keycloak/data/export
```

---

## 8. References
- [Keycloak Documentation](https://www.keycloak.org/documentation)
- [Keycloak Docker Image](https://hub.docker.com/r/keycloak/keycloak)
```

---
