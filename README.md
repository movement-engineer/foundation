# foundation
Foundational documents and information; includes tooling around managing the documentation and publication site

### Contributing

See [CONTRIBUTING.md](CONTRIBUTING.md) for more details on how to contribute.

#### Required tools

For development, you need:
- `git`
- `hugo`

For publication, you need:
- `docker` (Desktop or native linux)
- `git`
- `hugo`
- `kubectl`

#### Development

For local development, you only need `hugo server -D` for testing content and layout changes. `config.toml` changes are
out of scope for this document, but note the base URL can break the site if not coordinated with kubernetes (k8s) changes.

#### Publication

We are using the outof-coffee private registry for publication until a dedicated registry can be established.

You will need:

1. Cluster access to the k8s cluster (using doctl or other rbac authentication)
2. Docker credentials for the private registry (using doctl or token authentication)

Steps:

```shell script
# get deployment name from existing deployments
export DEPLOYMENT_NAME=$(kubectl get deployments | grep movement-engineer | awk '{print $1}')
docker build -t registry.digitalocean.com/outof-coffee/movement-engineer-foundation-site:latest .
docker push registry.digitalocean.com/outof-coffee/movement-engineer-foundation-site:latest
kubectl rollout restart $DEPLOYMENT_NAME
```

### Goals

The goals of this repository are two-fold:

1. Establish foundational documents for use by `movement-engineer` internally
2. Provide a boilerplate starting point for other movements to use for their foundation
