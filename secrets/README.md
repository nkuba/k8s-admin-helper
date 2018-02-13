# Secrets

A Secret is an object that contains a small amount of sensitive data such as a password, a token, or a key.

## Resources
* [Documentation](https://kubernetes.io/docs/concepts/configuration/secret/)
* [API Reference](https://kubernetes.io/docs/api-reference/v1.9/#secret-v1-core)

## Kubectl commands

`kubectl get secrets`

`kubectl create secret generic <SECRET_NAME> --from-file=<FILE_PATH>`

`kubectl create secret generic <SECRET_NAME> --from-literal=<KEY>=<VALUE>`

## Creating a Secret Manually
[Documentation](https://kubernetes.io/docs/concepts/configuration/secret/#creating-a-secret-manually)

### Encode a Secret
Encode text with base64:
```bash
$ echo -n "admin" | base64
YWRtaW4=
```

Create manifest for the secret:
```yaml
apiVersion: v1
kind: Secret
metadata:
  name: mysecret
data:
  username: YWRtaW4=
```

### Decode a Secret

```bash
$ echo "YWRtaW4=" | base64 --decode
admin
```

## Manifests

```yaml
apiVersion: v1
kind: Secret
metadata:
    name: manual-secret
data:
    username: YWRtaW4=
    password: MWYyZDFlMmU2N2Rm
```

## Use Secret in Pod
Sample manifest: [pod_secret.yaml](../pod/pod_secret.yaml)