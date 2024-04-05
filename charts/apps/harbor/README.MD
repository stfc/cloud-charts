======
Harbor
======

Note: This does not work with the current version of Harbor.
Instead the user must manually edit the deployment in the UI until we upgrade to 1.10.x or later.

Preparation
===========

This chart assumes you have the following:

- An existing external DB
- S3 compatible storage

Secrets
=======

The following secrets are required in the same namespace
- database-credentials
- s3-credentials

These must be manually created:

- Create a secret file with the following template in `/tmp`
(Details can be found in the existing secret vault)

```yaml
apiVersion: v1
kind: Secret
metadata:
  name: <secret_name>
  namespace: <namespace>
type: Opaque
stringData:
  FIELD_NAME_A: VALUE_A
  FIELD_NAME_B: VALUE_B
```

- Apply the secret to the namespace

```bash
kubectl create namespace <namespace>
kubectl apply -f /tmp/<secret_name>.yaml
```

database-credentials
--------------------

Within the secret the following fields are required:
- host_fqdn     # The FQDN to connect to the DB
- username      # The username to connect to the DB with
- password      # The password to connect to the DB with
- database      # The database name to connect to

s3-credentials
--------------

TODO
