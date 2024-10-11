# Exemples de mise en production

## CEN Nouvelle-Aquitaine


``` mermaid
stateDiagram-v2

  **LDAP** --> **GeoServer**
  **LDAP** --> PostgreSQL: *ldap2pg*
  **GeoServer** --> QGIS: *WFS/WMS*
  PostgreSQL --> QGIS: *PostGIS*
  state QGIS {
  QGIS_auth --> FluxCEN
  }
```