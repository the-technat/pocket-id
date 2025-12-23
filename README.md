# pocket-id

pocket-id.org instance hosted on fly.io

## Deployment

Initial deployment was done according to [this doc](https://fly.io/docs/launch/continuous-deployment-with-github-actions/). The workflow runs against the `prod` env on the `main` branch.

Some special configs for this deployment:

Before you initially deploy the app create an S3 bucket in the ui and add some secrets:

```console
fly secrets set ENCRYPTION_KEY=<openssl rand -base64 32> --stage
fly secrets set S3_ACCESS_KEY_ID=<define> --stage
fly secrets set S3_SECRET_ACCESS_KEY=<define> --stage
```
After the initial deployment a custom domain was provisioned according to [this doc](https://fly.io/docs/networking/custom-domain/).
For Pull Requests a review environment is automatically deployed.

Secrets have been all generated manually and added to this repository.
