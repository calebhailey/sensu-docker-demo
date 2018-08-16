# Overview

A simple sandbox environment for running Sensu on your local workstation via
Docker.

## Instructions

1. Set your Sensu Enterprise repository username and password as environment
   variables.

   ```
   $ export SENSU_ENTERPRISE_REPO_USERNAME=1234567890
   $ export SENSU_ENTERPRISE_REPO_PASSWORD=abcdefghijklmnop
   ```

2. Run `docker-compose up`.

   ```
   $ docker-compose up -d
   ```

3. Verify your working installation! Curl the API from your local workstation
   (optionally piping the output to [jq][jq]).

   ```
   $ curl -s http://localhost:4567/settings
   ```

   [jq]: https://stedolan.github.io/jq/
