# k8s-BookStack
Quickly deploy a BookStack wiki to your kubernetes cluster.

---

### Deployment:

0. Create a new namespace using `kubectl create ns newnamespace`.

   Use this namespace in all further `kubectl` commands by appending `-n newnamespace`.
1. Store your database credentials in a secret called `bookstack-database`. This command generates a random user password and root password.
```shell
kubectl create secret generic bookstack-database --from-literal password=$(cat /dev/urandom | env LC_CTYPE=C tr -dc a-zA-Z0-9 | head -c 32; echo) --from-literal root=$(cat /dev/urandom | env LC_CTYPE=C tr -dc a-zA-Z0-9 | head -c 32; echo) --from-literal username=bookstack-user
```
2. Deploy mariadb
```shell
kubectl apply -f mariadb.yaml
```
3. Deploy BookStack
```shell
kubectl apply -f bookstack.yaml
```

---
### Usage:
The default login is `admin@admin.com` with password `password`. Make sure to change your password.