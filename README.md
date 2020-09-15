## Usage


**IMPORTANT:** The `master` branch is used in `source` just as an example. In your code, do not pin to `master` because there may be breaking changes between releases.
Instead pin to the release tag (e.g. `?ref=tags/x.y.z`) of one of our [latest releases](https://github.com/alysonfranklin/ecs-service/releases).



[Basic example](examples/basic)

```hcl
module "my-service" {
  source                        = "github.com/alysonfranklin/ecs-service.git//?ref=1.0"
  VPC_ID                        = "vpc-9823742"
  APPLICATION_NAME              = "example-service"
  APPLICATION_PORT              = 8080
  APPLICATION_VERSION           = "latest"
  CREATE_ECR                    = true
  CLUSTER_ARN                   = data.aws_ecs_cluster.selected.arn
  SERVICE_ROLE_ARN              = data.aws_iam_role.selected.arn
  AWS_REGION                    = var.AWS_REGION
  HEALTHCHECK_MATCHER           = "200"
  HEALTH_CHECK_PATH             = "/"
  CPU_RESERVATION               = 500
  MEMORY_RESERVATION            = 256
  LOG_GROUP                     = "aws/ecs/example-service"
  DESIRED_COUNT                 = 2
  ALB_ARN                       = module.my-alb.alb_arn
  LOAD_BALANCING_ALGORITHM_TYPE = "round_robin"
  TARGET_GROUP_NAME             = "${var.APPLICATION_NAME}-tg"
  DEFAULT_TAGS                  = merge(var.DEFAULT_TAGS, { Name = "${var.DEFAULT_TAGS["Environment"]}-${var.APPLICATION_NAME}-tg" })
}
```


<!-- markdownlint-disable -->
## Makefile Targets
```text
Available targets:

  help                                Help screen
  help/all                            Display help for all targets
  help/short                          This help short screen
  lint                                Lint terraform code

```
<!-- markdownlint-restore -->
<!-- markdownlint-disable -->
## Requirements

| Name | Version |
|------|---------|
| terraform | >= 0.12.0 |
| aws | >= 2.0 |
| null | >= 2.0 |

## Providers

| Name | Version |
|------|---------|
| aws | >= 2.0 |

## Inputs

| Name | Description | Type | Default | Required |
|------|-------------|------|---------|:--------:|
| VPC\_ID | VPC ID. | `string` | `""` | yes |
| APPLICATION\_NAME | Service name in ECS | `string` | `""` | yes |
| APPLICATION\_PORT | Port number in target_group | `number` | `8080` | no |

## Outputs

| Name | Description |
|------|-------------|
| target_group_arn | Amazon Resource Name (ARN) of the target_group |

<!-- markdownlint-restore -->

### Developing

If you are interested in being a contributor and want to get involved in developing this project or help out with our other projects, we would love to hear from you!

In general, PRs are welcome. We follow the typical "fork-and-pull" Git workflow.

 1. **Fork** the repo on GitHub
 2. **Clone** the project to your own machine
 3. **Commit** changes to your own branch
 4. **Push** your work back up to your fork
 5. Submit a **Pull Request** so that we can review your changes

**NOTE:** Be sure to merge the latest changes from "upstream" before making a pull request!


## Copyright

Copyright © 2017-2020 [Alyson Franklin](https://www.linkedin.com/in/alysonfranklin)



## License

[![License](https://img.shields.io/badge/License-Apache%202.0-blue.svg)](https://opensource.org/licenses/Apache-2.0)

See [LICENSE](LICENSE) for full details.

```text
Licensed to the Apache Software Foundation (ASF) under one
or more contributor license agreements.  See the NOTICE file
distributed with this work for additional information
regarding copyright ownership.  The ASF licenses this file
to you under the Apache License, Version 2.0 (the
"License"); you may not use this file except in compliance
with the License.  You may obtain a copy of the License at

  https://www.apache.org/licenses/LICENSE-2.0

Unless required by applicable law or agreed to in writing,
software distributed under the License is distributed on an
"AS IS" BASIS, WITHOUT WARRANTIES OR CONDITIONS OF ANY
KIND, either express or implied.  See the License for the
specific language governing permissions and limitations
under the License.
```
