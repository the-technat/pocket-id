# pocket-id

pocket-id.org instance hosted on fly.io.

No real use-case for this but I lust love OIDC and especially pocket-id.

## Setup

Serverless Container with scale-to-zero capability. Starts whenever a request is made.

## State

User-uploads are stored in the referenced S3 bucket. Everything else is stored in an SQLite database.
For the sqlite file there is a persistent volume provisioned with automatic snapshots once a day. T
This will persist even if machines need to replaced

The keys are also stored in the database and encrypted with a provided key. This key should be kept safe in your password manager or similar.

## Backups

Missing: should we ever loose the volume we would loose all state. Need a way to dump the sqlite file to S3 or similar.

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
