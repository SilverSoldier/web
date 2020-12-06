# Gitea on OpenShift

## Air-gapped

```bash
oc image mirror \
    -a ${LOCAL_SECRET_JSON} \
    docker.io/gitea/gitea:latest \
    ${LOCAL_REGISTRY}/gitea/gitea:latest
```

oc process -f https://raw.githubusercontent.com/lathil/openshift-gitea/master/templates/gitea-persistent.yaml --parameters

oc process -f https://raw.githubusercontent.com/lathil/openshift-gitea/master/templates/gitea-persistent.yaml \
  -p GITEA_REPOS_URL=${LOCAL_REGISTRY}/gitea/gitea \
  -p ROOT_URL=apps.air-gapped.azure.openshift.pub \
  | oc apply -f -
