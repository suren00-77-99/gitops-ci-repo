# GitOps CI Repository

This repository builds and scans frontend/backend container images, pushes them to Amazon ECR,
and updates the GitOps repository with the new image tags.

## Pipeline flow

1. Checkout application source.
2. Build frontend image.
3. Build backend image.
4. Scan both images with Trivy.
5. Authenticate to AWS.
6. Push images to ECR.
7. Update the CD repository image tags.
8. Commit and push the change to the CD repository.
9. Argo CD detects the Git change and deploys automatically.

## Required GitHub Actions secrets

- `AWS_ACCESS_KEY_ID`
- `AWS_SECRET_ACCESS_KEY`
- `AWS_REGION`
- `ECR_REGISTRY`
- `ECR_FRONTEND_REPOSITORY`
- `ECR_BACKEND_REPOSITORY`
- `GITOPS_REPO_TOKEN`

`GITOPS_REPO_TOKEN` must be a GitHub fine-grained token with Contents: Read and write permission
for the CD repository.

## Example ECR values

```text
ECR_REGISTRY=123456789012.dkr.ecr.ap-south-1.amazonaws.com
ECR_FRONTEND_REPOSITORY=gitops/frontend
ECR_BACKEND_REPOSITORY=gitops/backend
AWS_REGION=ap-south-1
```
