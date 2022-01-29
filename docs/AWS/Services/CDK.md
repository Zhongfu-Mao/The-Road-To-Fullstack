# AWS Cloud Development Kit

## Basic Knowledge

### Layers of a CDK Application

* App: no CloudFormation equivalent
  * Stack: CloudFormation Stack
    * Nested Stack: CloudFormation Nested Stack
    * Construct: 1(or more) CloudFormation Resources
* Can have multiple App layers
* Apps can have multiple Stacks

!!!info

    The OUTPUT of CDK is CloudFormation

### CDK APP

* App is a special root Construct
* Orchestrate the lifecycle of the Stacks and Resources within it
* App Lifecyle:
  * Construct
  * Prepare
  * Validate
  * Synthesize
  * Deploy

### CDK Stack

* A CDK stack becomes a CloudFormation Stack
* Multiple Stacks can be created within a single App
* Stacks within the same App can ==share resources==
* CDK NestedStacks generate CloudFormation NestedStacks
  * Stacks with Stacks as Resources

### CDK Constructs

* Level 0: Basic Resource (no Type)
* Level 1: CloudFormation Resource (1:1)
  * These are pre-fixed with `Cfn` in the CDK API
* Level 2: Improved L1 Constructs
  * Provided by the CDK Team
  * Include helper methods and sensible defaults
* Level 3: Combinations of Constructs

!!!tip

    Most frequently L2/L3 Constucts are been used

### Assets

* Assets are files bundled into CDK apps
  * lambda handler code
  * Docker images
* Assets can represent any artifact that the app needs to operate
* When you synthesize or deploy a CDK app, these assets typically end up in `cdk.out`

### Bootstrapping

* Running `cdk bootstrap` deply a CDKToolkit CloudFormation Stack
* Create an S3 Bucket to store Assets in an AWS Account
* Required for ==Assets== and CloudFormation ==templates > 50KB==

## Reference
