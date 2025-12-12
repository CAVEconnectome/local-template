# Local CAVE Template

This repository contains Copier templates for creating CAVE local environments and clusters.

## Structure

- `environment-template/` - Creates the parent environment structure (root.hcl, scripts, static)
- `cluster-template/` - Creates cluster instances within an environment (helmfile, kubernetes, terragrunt.hcl)

## Usage

### Step 1: Create Environment Structure

First, create the parent environment structure:

```bash
copier copy environment-template ../terraform-cave-private/<environment_name>
```

Example:
```bash
copier copy environment-template ../terraform-cave-private/ltv
```

This creates:
- `ltv/root.hcl` - Environment-level Terragrunt configuration
- `ltv/scripts/` - Helper scripts
- `ltv/static/` - Static infrastructure configuration

### Step 2: Create Cluster Instances

Then, create each cluster instance within that environment:

```bash
copier copy cluster-template ../terraform-cave-private/<environment_name>/<cluster_prefix>
```

Examples:
```bash
# Create ltv7 cluster
copier copy cluster-template ../terraform-cave-private/ltv/ltv7

# Create ltv8 cluster
copier copy cluster-template ../terraform-cave-private/ltv/ltv8
```

This creates:
- `ltv/ltv7/helmfile/` - Helmfile configuration
- `ltv/ltv7/kubernetes/` - Kubernetes Terragrunt config
- `ltv/ltv7/terragrunt.hcl` - Cluster-level Terragrunt config

## Using from GitHub

If this template is in a GitHub repository, you can reference subdirectories:

```bash
# Create environment
copier copy gh:your-org/local-template/environment-template ../terraform-cave-private/ltv

# Create cluster
copier copy gh:your-org/local-template/cluster-template ../terraform-cave-private/ltv/ltv7
```

## Notes

- The `local_environment_name` in the cluster template must match the parent environment folder name
- Each cluster instance is independent and can have different configurations
- The environment structure is shared across all clusters in that environment

