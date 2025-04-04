---
title: Environment variables precedence
description: Scenario Overview illustrating how environment variables are resolved in Compose
keywords: compose, environment, env file
---

## Order of precedence
1. Passed from the command line [`docker compose run --env <KEY[=[VAL]]>`](../../engine/reference/commandline/compose_run/#options).
2. Passed from/set in `compose.yaml` service's configuration, from the [environment key](../../compose/compose-file/#environment).
3. Passed from/set in `compose.yaml` service's configuration, from the [env_file key](../../compose/compose-file/#env_file).
4. Passed from/set in Container Image in the [ENV directive](../../engine/reference/builder/#env).

### Precedence quick overview table
The table below provides a quick overview of how interpolation works when using environment variables on Compose.
This overview is done using `TAG`, an environment variable defining the version for an image, as an example.

Each table's:
* column - represents a context from where you can set or pass `TAG`, or environment variables in general.
* row - represents a scenario, this means a combination of contexts where `TAG` is set or passed simultaneously.

The last column gives you the final result: how `TAG` is resolved for each scenario according to the precedence rule.

|  # |  `run --env`  |  `compose.yaml`:`environment` key  |  `compose.yaml`:`env_file` key  |  Image `ENV` |  `Host OS` environment  |  `.env` file      |  RESOLVED AS  |
|:--:|:-------------:|:----------------------------------:|:-------------------------------:|:------------:|:-----------------------:|:-----------------:|:-------------:|
|  1 |   -           |   -                                |   -                             |   -          |  `TAG=1.4`              |  `TAG=1.3`        |   -           |
|  2 |   -           |   -                                |   -                             |**`TAG=1.5`** |  `TAG=1.4`              |  `TAG=1.3`        |**`TAG=1.5`**  |
|  3 |**`TAG`**      |   -                                |   -                             |  `TAG=1.5`   |**`TAG=1.4`**            |  `TAG=1.3`        |**`TAG=1.4`**  |
|  4 |   -           |   -                                |**`TAG`**                        |  `TAG=1.5`   |   -                     |**`TAG=1.3`**      |**`TAG=1.3`**  |
|  5 |**`TAG`**      |   -                                |   -                             |  `TAG=1.5`   |   -                     |**`TAG=1.3`**      |**`TAG=1.3`**  |
|  6 |**`TAG=1.8`**  |   -                                |   -                             |  `TAG=1.5`   |  `TAG=1.4`              |  `TAG=1.3`        |**`TAG=1.8`**  |
|  7 |   -           |**`TAG`**                           |   -                             |  `TAG=1.5`   |**`TAG=1.4`**            |  `TAG=1.3`        |**`TAG=1.4`**  |
|  8 |**`TAG`**      |  `TAG=1.7`                         |   -                             |  `TAG=1.5`   |**`TAG=1.4`**            |  `TAG=1.3`        |**`TAG=1.4`**  |
|  9 |**`TAG=1.8`**  |  `TAG=1.7`                         |   -                             |  `TAG=1.5`   |  `TAG=1.4`              |  `TAG=1.3`        |**`TAG=1.8`**  |
| 10 |   -           |**`TAG`**                           |   -                             |  `TAG=1.5`   |**`TAG=1.4`**            |  `TAG=1.3`        |**`TAG=1.4`**  |
| 11 |**`TAG=1.8`**  |   -                                |  `TAG=1.6`                      |  `TAG=1.5`   |  `TAG=1.4`              |  `TAG=1.3`        |**`TAG=1.8`**  |
| 12 |**`TAG=1.8`**  |  `TAG=1.7`                         |  `TAG=1.6`                      |  `TAG=1.5`   |  `TAG=1.4`              |  `TAG=1.3`        |**`TAG=1.8`**  |
| 13 |   -           |   -                                |**`TAG=1.6`**                    |  `TAG=1.5`   |  `TAG=1.4`              |   -               |**`TAG=1.6`**  |
| 14 |   -           |**`TAG=1.7`**                       |   -                             |  `TAG=1.5`   |  `TAG=1.4`              |   -               |**`TAG=1.7`**  |

Table column's description:
* `run --env` - environment variable set via the command line: `docker compose run -e <KEY[=[VAL]]>`.
* `compose.yaml`:`environment` key - In `environment` key from the service section in the `compose.yaml` file.
* `compose.yaml`:`env_file` key - In `env_file` key from the service section in the `compose.yaml` file.
* Image `ENV` - `ENV` directive in the Dockerfile for the image.
* `Host OS` environment - the environment where the Docker Engine is running.
* `.env` file - the `.env` file on the project root.
* RESOLVED AS - This column expresses the result available in the container. So this column expresses the value of `TAG`, our example in this table, after Compose applies the precedence rule.

> **Note**
>
> Obs: The columns "`Host OS` environment" and "`.env` file" are listed only for lookup. These columns cannot result in a variable in the container by itself.