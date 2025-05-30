# Plaid

## Overview

The Plaid source supports Full Refresh syncs. It currently only supports pulling from the balances endpoint. It will soon support other data streams \(e.g. transactions\).

### Output schema

Output streams:

- [Balance](https://plaid.com/docs/api/products/#balance)

### Features

| Feature                       | Supported?  |
| :---------------------------- | :---------- |
| Full Refresh Sync             | Yes         |
| Incremental - Append Sync     | Coming soon |
| Replicate Incremental Deletes | Coming soon |
| SSL connection                | Yes         |
| Namespaces                    | No          |

### Performance considerations

The Plaid connector should not run into Stripe API limitations under normal usage. Please [create an issue](https://github.com/airbytehq/airbyte/issues) if you see any rate limit issues that are not automatically retried successfully.

## Getting started

### Requirements

- Plaid Account \(with client_id and API key\)
- Access Token

### Setup guide for Sandbox

This guide will walk through how to create the credentials you need to run this source in the sandbox of a new plaid account. For production use, consider using the Link functionality that Plaid provides [here](https://plaid.com/docs/api/tokens/#linktokencreate)

- **Create a Plaid account** Go to the [plaid website](https://plaid.com/) and click "Get API Keys". Follow the instructions to create an account.
- **Get Client id and API key** Go to the [keys page](https://dashboard.plaid.com/team/keys) where you will find the client id and your Sandbox API Key \(in the UI this key is just called "Sandbox"\).
- **Create an Access Token** First you have to create a public token key and then you can create an access token.

  - **Create public key** Make this API call described in [plaid docs](https://plaid.com/docs/api/sandbox/#sandboxpublic_tokencreate)

    ```bash
      curl --location --request POST 'https://sandbox.plaid.com/sandbox/public_token/create' \
          --header 'Content-Type: application/json;charset=UTF-16' \
          --data-raw '{
              "client_id": "<your-client-id>",
              "secret": "<your-sandbox-api-key>",
              "institution_id": "ins_127287",
              "initial_products": ["auth", "transactions"]
          }'
    ```

  - **Exchange public key for access token** Make this API call described in [plaid docs](https://plaid.com/docs/api/tokens/#itempublic_tokenexchange). The public token used in this request, is the token returned in the response of the previous request. This request will return an `access_token`, which is the last field we need to generate for the config for this source!

    ```bash
    curl --location --request POST 'https://sandbox.plaid.com/item/public_token/exchange' \
      --header 'Content-Type: application/json;charset=UTF-16' \
      --data-raw '{
          "client_id": "<your-client-id>",
          "secret": "<your-sandbox-api-key>",
          "public_token": "<public-token-returned-by-previous-request>"
      }'
    ```

- We should now have everything we need to configure this source in the UI.

## Changelog

<details>
  <summary>Expand to review</summary>

| Version | Date       | Pull Request                                             | Subject                                                       |
| :------ | :--------- | :------------------------------------------------------- | :------------------------------------------------------------ |
| 0.5.14 | 2025-05-10 | [60070](https://github.com/airbytehq/airbyte/pull/60070) | Update dependencies |
| 0.5.13 | 2025-05-03 | [59498](https://github.com/airbytehq/airbyte/pull/59498) | Update dependencies |
| 0.5.12 | 2025-04-27 | [59039](https://github.com/airbytehq/airbyte/pull/59039) | Update dependencies |
| 0.5.11 | 2025-04-19 | [58455](https://github.com/airbytehq/airbyte/pull/58455) | Update dependencies |
| 0.5.10 | 2025-04-12 | [57876](https://github.com/airbytehq/airbyte/pull/57876) | Update dependencies |
| 0.5.9 | 2025-04-05 | [57333](https://github.com/airbytehq/airbyte/pull/57333) | Update dependencies |
| 0.5.8 | 2025-03-29 | [56804](https://github.com/airbytehq/airbyte/pull/56804) | Update dependencies |
| 0.5.7 | 2025-03-22 | [56173](https://github.com/airbytehq/airbyte/pull/56173) | Update dependencies |
| 0.5.6 | 2025-03-08 | [55535](https://github.com/airbytehq/airbyte/pull/55535) | Update dependencies |
| 0.5.5 | 2025-03-01 | [55004](https://github.com/airbytehq/airbyte/pull/55004) | Update dependencies |
| 0.5.4 | 2025-02-23 | [54575](https://github.com/airbytehq/airbyte/pull/54575) | Update dependencies |
| 0.5.3 | 2025-02-15 | [53973](https://github.com/airbytehq/airbyte/pull/53973) | Update dependencies |
| 0.5.2 | 2025-02-08 | [47502](https://github.com/airbytehq/airbyte/pull/47502) | Update dependencies |
| 0.5.1 | 2024-08-16 | [44196](https://github.com/airbytehq/airbyte/pull/44196) | Bump source-declarative-manifest version |
| 0.5.0 | 2024-08-14 | [44086](https://github.com/airbytehq/airbyte/pull/44086) | Refactor connector to manifest-only format |
| 0.4.13 | 2024-08-12 | [43861](https://github.com/airbytehq/airbyte/pull/43861) | Update dependencies |
| 0.4.12 | 2024-08-10 | [43663](https://github.com/airbytehq/airbyte/pull/43663) | Update dependencies |
| 0.4.11 | 2024-08-03 | [43239](https://github.com/airbytehq/airbyte/pull/43239) | Update dependencies |
| 0.4.10 | 2024-07-27 | [42686](https://github.com/airbytehq/airbyte/pull/42686) | Update dependencies |
| 0.4.9 | 2024-07-20 | [42230](https://github.com/airbytehq/airbyte/pull/42230) | Update dependencies |
| 0.4.8 | 2024-07-13 | [41730](https://github.com/airbytehq/airbyte/pull/41730) | Update dependencies |
| 0.4.7 | 2024-07-10 | [41412](https://github.com/airbytehq/airbyte/pull/41412) | Update dependencies |
| 0.4.6 | 2024-07-09 | [41235](https://github.com/airbytehq/airbyte/pull/41235) | Update dependencies |
| 0.4.5 | 2024-07-06 | [41007](https://github.com/airbytehq/airbyte/pull/41007) | Update dependencies |
| 0.4.4 | 2024-06-25 | [40379](https://github.com/airbytehq/airbyte/pull/40379) | Update dependencies |
| 0.4.3 | 2024-06-22 | [40147](https://github.com/airbytehq/airbyte/pull/40147) | Update dependencies |
| 0.4.2 | 2024-06-04 | [38963](https://github.com/airbytehq/airbyte/pull/38963) | [autopull] Upgrade base image to v1.2.1 |
| 0.4.1 | 2024-05-31 | [38810](https://github.com/airbytehq/airbyte/pull/38810) | [autopull] Migrate to base image and poetry |
| 0.4.0 | 2023-08-17 | [29127](https://github.com/airbytehq/airbyte/pull/29127) | Rewrote connector to no-code SDK |
| 0.3.2 | 2022-08-02 | [15231](https://github.com/airbytehq/airbyte/pull/15231) | Added min_last_updated_datetime support for Capital One items |
| 0.3.1 | 2022-03-31 | [11104](https://github.com/airbytehq/airbyte/pull/11104) | Fix 100 record limit and added start_date |
| 0.3.0 | 2022-01-05 | [7977](https://github.com/airbytehq/airbyte/pull/7977) | Migrate to Python CDK + add transaction stream |

</details>
