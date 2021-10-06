# Automated k6 load testing with Atlassian Bamboo

This is an example repo for how to setup k6 with [Atlassian Bamboo](https://www.atlassian.com/software/bamboo) CI/CD to build load testing into an automation flow.

The full guide describing how to use this repository is located [here](https://blog.loadimpact.com/).

## Examples

Bamboo [yaml spec](https://confluence.atlassian.com/bamboo/bamboo-yaml-specs-938844479.html) files need to be placed in `bamboo-specs/bamboo.yml` or `bamboo-specs/bamboo.yaml`. The example configurations below were generated via Bamboo's user interface.

Do note these configurations are provided as examples and will not work out-of-the-box on your Bamboo server instance. You'll need at least to create the project manually and update the `users` section.

| File                                                   | Description                        |
| ------------------------------------------------------ | ---------------------------------- |
| [local-example/bamboo.yaml](local-example/bamboo.yaml) | Runs locally on AWS infrastructure |
| [cloud-example/bamboo.yaml](cloud-example/bamboo.yaml) | Runs on k6 cloud                   |

## Run Local

```bash
# Run locally
k6 run scripts/test.js

# Run via Docker
docker run -i loadimpact/k6 run - <scripts/test.js
```

## Run Cloud

```bash
# Run directly
k6 login cloud --token <YOUR_K6_CLOUD_API_TOKEN>
k6 cloud scripts/cloud-test.js

# Run via Docker
docker run -i -e K6_CLOUD_TOKEN=<API_TOKEN> loadimpact/k6 cloud - <scripts/cloud-test.js

# Alternative Docker version with mounting option
docker run -i -e K6_CLOUD_TOKEN=<API_TOKEN> -v "$PWD/scripts:/cloud-test.js" loadimpact/k6 cloud /cloud-test.js
```
