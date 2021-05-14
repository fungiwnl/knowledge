# Infrastructure as Code

- Without IaC, we do a lot of manual work
- All this manual work will be very tough to reproduce
   - In another region,
   - In another AWS Account
   - Within the same region if everything was deleted

- IaC is the concept that code would be deploy4ed to create / update/ delete infrastructure

## Cloudformation

- CloudFormation is a declarative way of outlining your AWS Infrastrucutre, for any resources (most of them are supported).
- For example within a CF tempalte you say:
   - I want a security group
   - I want two EC2 machines using this security group
   - I want two Elastic IPs for these EC2 machines
   - I want an S3 bucket 
   - I want a load balancer (ELB) for all these machines

- Then CF creates those for  you, in the right order, with the exact config you specify

## Benefits

- IaC
  - No resource are manually created, which is excellent for control
  - The code can be version controlled using git
  - Changes to the infra are reviewed through code

- Cost
  - Each resources within the stack is tagged with an identifier so you can easily see how much a stack costs you
  - You can estimate the costs of your resources using the CF template
  - Saving strategy: In Dev, you could auto delete templates at 5PM and and recreated at 8AM safely 

- Productivity
  - Ability to destroy and re-create an infra on the cloud on the fly
  - Automated generation of Diagram for your tempaltes
  - Declarative programming (no need to figure out ordering and orchestation

- Seperation of concern: createm any stacks for many apps, and many layers Ex:
  - VPC stacks
  - Network stacks
  - App stacks 

- Don't re-invent the wheel
  - Leverage existing templates on the web! 


## How it works

- Templates have to be uploaded in S3 and then referenced in CloudFormation
- To update a template we cant edit previous ones. We have to re-upload a new version of the template to AWS
- Stacks are identified by a name
- Deleting a stack deletes every single artifact that was created by CF

### Deploying 

- Manual way:
  - Editing templates in the cloudformation designer
  - Using the console to input parameters, etc

- Autoamted way
  - Editing templates in a YAML
  - Using a AWS CLI to deploy the templates
  - Recommend way when you fully automate your templates

### Building blocks

- Template components:

1. Resources: your AWS resources declared in the template (mandatory)
2. Parameters: the dynamic inputs for your template
3. Mappings: the static variables for your tempalte
4. Outputs: references to what has been created
5. Conditionals: list of conditions to perform resource creation 
6. Metadata 

- Template helpers:

1. Reference
2. Functions


## Practical

```yml
Resources:
  MyInstance:
    Type: AWS::EC2::Instance
    Properties: 
      AvailabilityZone: ap-southeast-2
      ImageId: ami-a4c7edb2
      InstanceType: t2.micro
```

## StackSets

- Create, update, or delete stacks across multiple accounts and regions with a single operation
- Admin account to create StackSets
- Trusted accounts to create, update, delete stack instance from StackSets
- When you update a stack set, all associated stack instances are  updated throughout all accounts and regions
