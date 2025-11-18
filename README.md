# Terraform Provider Sample
Sample using Fractal Cloud Terraform Provider to initialize Environments and Fractals, as an alternative to use the Java SDK as shown [in this example](https://github.com/Fractal-Cloud/automotive-with-fractal-cloud).

The goal of Fractal Cloud is to simplify, standardize and govern infrastructure at scale. Achieving this depends on whether Ops and Dev teams can work together in a consistent and efficient way.

This example shows how Ops teams can use the technology they already know to define Fractals, namely Terraform HCL, while developers consume them through the tools and languages they prefer such as Java, C# or Typescript. This creates a shared model where infrastructure is governed by design and developers can move without friction.

## Code organization

In the `provider.tf` file you can initialize the provider using the Service Account ID and Secret you can find using the Fractal Cloud Web UI.
![Initialize a Service account](docs/accountCiCdServiceAccount.png)

These information can also be provided through the use of the `FRACTAL_CLOUD_SERVICE_ACCOUNT_ID` and `FRACTAL_CLOUD_SERVICE_ACCOUNT_SECRET` evironment variables.

In the `resource-groups.tf` file you will find the Resource Groups defined to segment your IT Landscape in different zones so that different teams have access to different portion of your infrastructure.

To use this sample, you should substitute the `owner_id` with the one found through the Fractal Cloud Web UI, as shown in the screenshot below:

![Initialize a Service account](docs/copyAccountId.png)

The `environments.tf` and `fractals.tf` contains the definition of Environments and Fractals respectively.

## Output:

As an example, the output of such a plan should be:

```terraform
Terraform used the selected providers to generate the following execution plan. Resource actions are indicated with the following symbols:
  + create

Terraform will perform the following actions:

  # fractalcloud_fractal.containerized will be created
  + resource "fractalcloud_fractal" "containerized" {
      + blueprint_components = [
          + {
              + display_name = "Kubernetes cluster for workloads"
              + id           = "k8s-containerized"
              + links        = []
              + locked       = false
              + parameters   = {
                  + "apiGateway" = {},
                  + "logging"    = {},
                  + "monitoring" = {},
                }
              + type         = "NetworkAndCompute.PaaS.ContainerPlatform"
              + version      = "1.2.12"
            },
        ]
      + created_at           = (known after apply)
      + created_by           = (known after apply)
      + description          = "Microservice Fractal for our Organization"
      + id                   = (known after apply)
      + interface_operations = [
          + {
              + instructions = [
                  + {
                      + component_id     = "k8s-containerized"
                      + input_parameters = [
                          + "workload",
                        ]
                      + operation        = "withWorkload"
                    },
                  + {
                      + component_id     = "k8s-containerized"
                      + input_parameters = [
                          + "externalDns",
                          + "workload",
                        ]
                      + operation        = "exposeService"
                    },
                ]
              + name         = "withExposedWorkload"
              + parameters   = [
                  + "workload, externalDns",
                ]
            },
        ]
      + resource_group_id    = (known after apply)
      + status               = (known after apply)
      + updated_at           = (known after apply)
      + updated_by           = (known after apply)
      + version              = "1.0"
    }

  # fractalcloud_management_environment.production will be created
  + resource "fractalcloud_management_environment" "production" {
      + azure_agent     = {
          + region          = "westeurope"
          + subscription_id = "xxx"
          + tenant_id       = "xxx"
        }
      + created_at      = (known after apply)
      + created_by      = (known after apply)
      + display_name    = "Production"
      + gcp_agent       = {
          + organization_id = "xxx"
          + project_id      = "xxx"
          + region          = "europe-west3"
        }
      + id              = (known after apply)
      + owner_id        = "xxx"
      + resource_groups = [
          + (known after apply),
        ]
      + status          = (known after apply)
      + type            = "Personal"
      + updated_at      = (known after apply)
      + updated_by      = (known after apply)
    }

  # fractalcloud_operational_environment.audi_production will be created
  + resource "fractalcloud_operational_environment" "audi_production" {
      + agents                    = [
          + "Azure",
        ]
      + created_at                = (known after apply)
      + created_by                = (known after apply)
      + display_name              = "Audi Production"
      + id                        = (known after apply)
      + management_environment_id = (known after apply)
      + resource_groups           = [
          + (known after apply),
        ]
      + status                    = (known after apply)
      + updated_at                = (known after apply)
      + updated_by                = (known after apply)
    }

  # fractalcloud_operational_environment.toyota_production will be created
  + resource "fractalcloud_operational_environment" "toyota_production" {
      + agents                    = [
          + "Gcp",
        ]
      + created_at                = (known after apply)
      + created_by                = (known after apply)
      + display_name              = "Toyota Production"
      + id                        = (known after apply)
      + management_environment_id = (known after apply)
      + resource_groups           = [
          + (known after apply),
        ]
      + status                    = (known after apply)
      + updated_at                = (known after apply)
      + updated_by                = (known after apply)
    }

  # fractalcloud_resource_group.production will be created
  + resource "fractalcloud_resource_group" "production" {
      + created_at   = (known after apply)
      + created_by   = (known after apply)
      + display_name = "Production"
      + id           = (known after apply)
      + owner_id     = "xxx"
      + type         = "Personal"
      + updated_at   = (known after apply)
      + updated_by   = (known after apply)
    }

  # fractalcloud_resource_group.production_audi will be created
  + resource "fractalcloud_resource_group" "production_audi" {
      + created_at   = (known after apply)
      + created_by   = (known after apply)
      + display_name = "Audi Production"
      + id           = (known after apply)
      + owner_id     = "xxx"
      + type         = "Personal"
      + updated_at   = (known after apply)
      + updated_by   = (known after apply)
    }

  # fractalcloud_resource_group.production_toyota will be created
  + resource "fractalcloud_resource_group" "production_toyota" {
      + created_at   = (known after apply)
      + created_by   = (known after apply)
      + display_name = "Toyota Production"
      + id           = (known after apply)
      + owner_id     = "xxx"
      + type         = "Personal"
      + updated_at   = (known after apply)
      + updated_by   = (known after apply)
    }

Plan: 7 to add, 0 to change, 0 to destroy.
```