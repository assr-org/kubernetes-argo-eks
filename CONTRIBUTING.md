# Contributing

Thanks for your interest in improving this project.

## How to contribute

1. Fork the repository and create a feature branch.
2. Make your changes in a focused, reviewable commit.
3. Validate the change locally before submitting a pull request.
4. Open a pull request with a clear description of what changed and why.

## Local validation

For code or content changes, verify the app still builds correctly:

```bash
docker build -t kubernetes-argo-eks:local .
```

If you change Kubernetes manifests, validate them with:

```bash
kubectl apply --dry-run=client -f k8s/
```

## Pull request expectations

- Keep changes small and targeted.
- Update documentation when behavior, deployment steps, or configuration changes.
- Include a short summary and testing notes in the PR description.
- Ensure the repo remains easy to understand for a GitOps/EKS demo use case.

## Code review

This repository uses CODEOWNERS to route review requests to the maintainers. Please be patient while maintainers review pull requests and provide feedback.
