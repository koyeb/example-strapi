<div align="center">
  <a href="https://koyeb.com">
    <img src="https://www.koyeb.com/static/images/icons/koyeb.svg" alt="Logo" width="80" height="80">
  </a>
  <h3 align="center">Koyeb Serverless Platform</h3>
  <p align="center">
    Deploy Strapi on Koyeb
    <br />
    <a href="https://koyeb.com">Learn more about Koyeb</a>
    ·
    <a href="https://koyeb.com/docs">Explore the documentation</a>
    ·
    <a href="https://koyeb.com/tutorials">Discover our tutorials</a>
  </p>
</div>


## About Koyeb and the Strapi example application

Koyeb is a developer-friendly serverless platform to deploy apps globally. No-ops, servers, or infrastructure management.

This repository contains is designed to show how to deploy a production-ready Strapi instance to Koyeb.  The repository defines a few example content types and includes configuration to upload assets to object storage.

## Getting Started

Follow the steps below to deploy the Strapi application to your Koyeb account.

### Requirements

To use this repository, you need:

* A Koyeb account to build and run the application.  If you don't already have an account, you can [sign-up for free](https://app.koyeb.com/auth/signup).
* An external PostgreSQL database to store application data. You can use [Koyeb's PostgreSQL database](https://www.koyeb.com/docs/databases) to provision a PostgreSQL database for free.
* An object storage bucket.  [Backblaze B2](https://www.backblaze.com/cloud-storage) has a free usage allowance that can be used for this.

### Deploy using the Koyeb button

The fastest way to deploy the Strapi application is to click the **Deploy to Koyeb** button below.

[![Deploy to Koyeb](https://www.koyeb.com/static/images/deploy/button.svg)](https://app.koyeb.com/deploy?name=example-strapi&type=git&repository=koyeb%2Fexample-strapi&branch=main&builder=buildpack&instance_type=eco-medium&env%5BADMIN_JWT_SECRET%5D=CHANGE_ME&env%5BAPI_TOKEN_SALT%5D=CHANGE_ME&env%5BAPP_KEYS%5D=CHANGE_ME&env%5BDATABASE_CLIENT%5D=postgres&env%5BDATABASE_URL%5D=CHANGE_ME&env%5BHOST%5D=0.0.0.0&env%5BJWT_SECRET%5D=CHANGE_ME&env%5BNODE_ENV%5D=production&env%5BS3_ACCESS_KEY_ID%5D=CHANGE_ME&env%5BS3_ACCESS_SECRET%5D=CHANGE_ME&env%5BS3_BUCKET%5D=CHANGE_ME&env%5BS3_ENDPOINT%5D=CHANGE_ME&env%5BS3_REGION%5D=CHANGE_ME&env%5BTRANSFER_TOKEN_SALT%5D=CHANGE_ME&ports=8000%3Bhttp%3B%2F)

Clicking on this button brings you to the Koyeb App creation page with most of the settings pre-configured to launch this application.  You will need to set the values for the following variables:

- `HOST`: Set to `0.0.0.0`. This tells Strapi to listen for connections on all interfaces.
- `NODE_ENV`: Set to `production`. This disables development-only features and enables our production-specific configuration.
- `DATABASE_CLIENT`: Set to `postgres` to use a PostgreSQL database instead of a local SQLite database.
- `DATABASE_URL`: The connection string to connect to and authenticate with the PostgreSQL database. Set this to the `psql` connection string you copied from your Koyeb database detail page and append `?ssl_mode=require` to the end to force the connection to use TLS/SSL.
- `S3_ENDPOINT`: The object storage bucket endpoint URL. Enter the "Endpoint" value you copied from Backblaze B2 (this should not include a protocol specification).
- `S3_REGION`: The region where the object storage bucket is hosted. Enter the region embedded in the endpoint URL. For instance if the `S3_ENDPOINT` is `s3.eu-central-003.backblazeb2.com`, the `S3_REGION` should be set to `eu-central-003`.
- `S3_BUCKET`: The name of your object storage bucket. Enter the bucket name copied from Backblaze B2.
- `S3_ACCESS_KEY_ID`: The key ID to use when authenticating to Backblaze B2. Enter the `keyID` for the API key that you created in Backblaze.
- `S3_ACCESS_SECRET`: The secret key to use when authenticating to Backblaze B2. Enter the `applicationKey` for the API key that you created in Backblaze.
- `APP_KEYS`: A comma-separated list of application keys to be used by middleware. Generate these with `openssl rand -base64 32`. For example, to set two keys, it might look like: `APP_KEYS=<first_key>,<second_key>`.
- `API_TOKEN_SALT`: The salt used to generate new API keys. Generate with `openssl rand -base64 32`.
- `JWT_SECRET`: A random string used to create new JSON Web Tokens (JWT). Generate with `openssl rand -base64 32`.
- `ADMIN_JWT_SECRET`: A separate random string used to create new JSON Web Tokens (JWT) for the admin panel. Generate with `openssl rand -base64 32`.
- `TRANSFER_TOKEN_SALT`: A salt used to generate [transfer tokens](https://docs.strapi.io/dev-docs/data-management/transfer#generate-a-transfer-token). Generate with `openssl rand -base64 32`.

_To modify this application example, you will need to fork this repository. Checkout the [fork and deploy](#fork-and-deploy-to-koyeb) instructions._

### Fork and deploy to Koyeb

If you want to customize and enhance this application, you need to fork this repository.

If you used the **Deploy to Koyeb** button, you can simply link your service to your forked repository to be able to push changes.  Alternatively, you can manually create the application as described below.

On the [Koyeb Control Panel](https://app.koyeb.com/), on the **Overview** tab, click the **Create Web Service** button to begin.

1. Select **GitHub** as the deployment method.
2. Choose the repository containing your application code.
3. Expand the **Environment variables** section and click **Bulk edit** to configure new environment variables.  Paste the following variable definitions in the box:
    ```
    HOST=0.0.0.0
    NODE_ENV=production
    DATABASE_CLIENT=postgres
    DATABASE_URL=
    S3_ENDPOINT=
    S3_REGION=
    S3_BUCKET=
    S3_ACCESS_KEY_ID=
    S3_ACCESS_SECRET=
    APP_KEYS=
    API_TOKEN_SALT=
    JWT_SECRET=
    ADMIN_JWT_SECRET=
    TRANSFER_TOKEN_SALT=
    ```

    Fill out the values as described in the previous section.

4. In the **Instance** section, select the **Eco** category and choose **eMedium** or larger. Strapi [recommends a single core and 2GB of memory](https://docs.strapi.io/dev-docs/deployment#hardware-and-software-requirements) at a minimum.
5. Choose a name for your App and Service, for example `example-strapi`, and click **Deploy**.

The repository will be pulled, built, and deployed on Koyeb. Once the deployment is complete, it will be accessible using the Koyeb subdomain for your service.

Use the following paths to interact with your instance:

* `/admin`: to access the admin panel and configure and publish content.
* `/api`: to access the content through the REST API.

## Contributing

If you have any questions, ideas or suggestions regarding this application sample, feel free to open an [issue](//github.com/koyeb/example-strapi/issues) or fork this repository and open a [pull request](//github.com/koyeb/example-strapi/pulls).

## Contact

[Koyeb](https://www.koyeb.com) - [@gokoyeb](https://twitter.com/gokoyeb) - [Slack](http://slack.koyeb.com/)
