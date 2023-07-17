# ADO Pipeline Template for Snyk IAC Test

This template uses azure pipeline to test iac based code like terraform.

* **NOTE:** As per today of July 13 2023, the snyk task available at marketplace azure, does not support iac testing so directly used script

## Pipeline Requirements

The Snyk Module pipeline requires the following parameters to be defined:

Parameters:

| Name  | Displayname | type | Default | Values | Opional/Required | Comments |
| ------------- | ------------- | ------------- | ------------- | ------------- | ------------- | ------------- |
| snykToken | The snyk authentication API token | string | | | Optional | Required when **testType=iac** |
| moduleLocation  | location of modules of terraform | string | | | Optional | Required when **testType=iac** |
--------------------------------------------------------------------------------------------------------------------------------------------------

## Use Cases

### Snyk Test for Terraform / Infracstucture as a Code

    ```yaml
    # azure-pipeline.yml
    resources:
        repositories:
        - repository: Snyk
            type: github
            name: knoldus/azurepipeline.snyk.iac
            ref: <respective branch name>
            endpoint: 'Duck Creek'

    steps:
    - template: iacTest.yml@Snyk
        parameters:
            snykToken: '$(snyk-token)'
            moduleLocation: './module'
    ```
