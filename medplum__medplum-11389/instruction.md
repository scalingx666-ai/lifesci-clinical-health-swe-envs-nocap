# Issue

**Title:** fix(cdk): resolve synth warnings

## Description

Fixed a bunch of deprecation warnings in CDK

- Use Stack#addStackDependency instead of deprecated addDependency
- Enable ECS deployment circuit breaker with rollback on Fargate services
- Acknowledge imported-bucket OAI policy warning; non-us-east-1 deployments apply the bucket policy via `medplum aws update-bucket-policies`

Before:

```bash
$ AWS_PROFILE=medplum-dev npm run staging:diff

> medplum-cdk-config@1.0.0 staging:diff
> cdk diff --context config=medplum.staging.config.json

[WARNING] aws-cdk-lib.Stack#addDependency is deprecated, and will be removed in the next major release.
  Use `addStackDependency` instead.
Stack ${Token[AWS::StackId.550]}
WARNING Enable the 'circuitBreaker' property to trigger a quicker deployment failure if tasks are failing to start up (without this setting deployments may take up to 3 hours to fail). (Construct Annotations)
   MedplumStaging/BackEnd/FargateService
   Acknowledge with 'Annotation::@aws-cdk/aws-ecs:shouldUseCircuitBreaker'

WARNING Enable the 'circuitBreaker' property to trigger a quicker deployment failure if tasks are failing to start up (without this setting deployments may take up to 3 hours to fail). (Construct Annotations)
   MedplumStaging/BackEnd/BackgroundJobsWorkerFargateService
   Acknowledge with 'Annotation::@aws-cdk/aws-ecs:shouldUseCircuitBreaker'

WARNING Cannot update bucket policy of an imported bucket. You will need to update the policy manually instead.
See the "Setting up OAI with imported S3 buckets (legacy)" section of module's README for more info. (Construct Annotations)
   MedplumStaging-us-east-1/FrontEnd/AppDistribution/Origin1
   Acknowledge with 'Annotation::@aws-cdk/aws-cloudfront-origins:updateImportedBucketPolicyOai'

WARNING Cannot update bucket policy of an imported bucket. You will need to update the policy manually instead.
See the "Setting up OAI with imported S3 buckets (legacy)" section of module's README for more info. (Construct Annotations)
   MedplumStaging-us-east-1/Storage/StorageDistribution/Origin1
   Acknowledge with 'Annotation::@aws-cdk/aws-cloudfront-origins:updateImportedBucketPolicyOai'
start: Building MedplumStaging Template
success: Built MedplumStaging Template
start: Publishing MedplumStaging Template (462446642923-us-west-2-81df929a)
success: Published MedplumStaging Template (462446642923-us-west-2-81df929a)
Hold on while we create a read-only change set to get a diff with accurate replacement information (use --method=template to use a less accurate but faster template-only diff)

Stack MedplumStaging (aws://462446642923/us-west-2)
There were no differences

start: Building MedplumStaging-us-east-1 Template
success: Built MedplumStaging-us-east-1 Template
start: Publishing MedplumStaging-us-east-1 Template (462446642923-us-east-1-c164ded6)
success: Published MedplumStaging-us-east-1 Template (462446642923-us-east-1-c164ded6)
Hold on while we create a read-only change set to get a diff with accurate replacement information (use --method=template to use a less accurate but faster template-only diff)

Stack MedplumStaging-us-east-1 (aws://462446642923/us-east-1)
There were no differences

✨  Number of stacks with differences: 0
```

After:

```bash
$ AWS_PROFILE=medplum-dev npm run staging:diff

> medplum-cdk-config@1.0.0 staging:diff
> cdk diff --context config=medplum.staging.config.json

Stack ${Token[AWS::StackId.553]}
start: Building MedplumStaging Template
success: Built MedplumStaging Template
start: Publishing MedplumStaging Template (462446642923-us-west-2-c50ca3e6)
success: Published MedplumStaging Template (462446642923-us-west-2-c50ca3e6)
Hold on while we create a read-only change set to get a diff with accurate replacement information (use --method=template to use a less accurate but faster template-only diff)

Stack MedplumStaging (aws://462446642923/us-west-2)
There were no differences

start: Building MedplumStaging-us-east-1 Template
success: Built MedplumStaging-us-east-1 Template
start: Publishing MedplumStaging-us-east-1 Template (462446642923-us-east-1-c164ded6)
success: Published MedplumStaging-us-east-1 Template (462446642923-us-east-1-c164ded6)
Hold on while we create a read-only change set to get a diff with accurate replacement information (use --method=template to use a less accurate but faster template-only diff)

Stack MedplumStaging-us-east-1 (aws://462446642923/us-east-1)
There were no differences

✨  Number of stacks with differences: 0
```

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `564ed95b4c13`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.