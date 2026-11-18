# Issue

**Title:** feat(infra): update removal policy of mllp server repo to make booting stack up / down easy

## Description

### Dependencies

None

### Description

This PR updates the existing ECR repo with a removal policy so that booting down the stack also wipes the ECR repo. This is fine as cdk should deploy a new ECR repo and part of the process is running a script to publish an image to the repo.

Here's the diff output against production - ignore some of the noise, its due to running diff from dev env as opposed to cloud env.
```
Resources
[~] AWS::ECR::Repository MllpServerRepo MllpServerRepo71CD67DD
 ├─ [+] EmptyOnDelete
 │   └─ true
 ├─ [~] DeletionPolicy
 │   ├─ [-] Retain
 │   └─ [+] Delete
 └─ [~] UpdateReplacePolicy
     ├─ [-] Retain
     └─ [+] Delete



[~] AWS::CloudFormation::Stack NestedMllpStack.NestedStack/NestedMllpStack.NestedStackResource NestedMllpStack
 └─ [~] TemplateURL
     └─ [~] .Fn::Join:
         └─ @@ -5,6 +5,6 @@
            [ ]     {
            [ ]       "Ref": "AWS::URLSuffix"
            [ ]     },
            [-]     "/cdk-hnb659fds-assets-463519787594-us-west-1/862948de67b0208f584fa48b97ccee321792d0f807460cb3a2a40e9e282973ca.json"
            [+]     "/cdk-hnb659fds-assets-463519787594-us-west-1/7a5962361867bb999eb9510369d296cab9f1d24ec446b333f0cbbcb1967528e4.json"
            [ ]   ]
            [ ] ]
[~] AWS::CloudFormation::Stack NestedNetworkStack.NestedStack/NestedNetworkStack.NestedStackResource NestedNetworkStack
 └─ [~] TemplateURL
     └─ [~] .Fn::Join:
         └─ @@ -5,6 +5,6 @@
            [ ]     {
            [ ]       "Ref": "AWS::URLSuffix"
            [ ]     },
            [-]     "/cdk-hnb659fds-assets-463519787594-us-west-1/ad9795a19678add106ae0de106763e7f0cd18c651637d2e5e5743b7534b9faf0.json"
            [+]     "/cdk-hnb659fds-assets-463519787594-us-west-1/b35bfe012a02cad1636cd2f46e2cf9a40553a2830f393fe7acef94e3f4abc345.json"
            [ ]   ]
            [ ] ]

Stack Hl7NotificationStack-NestedMllpStack-7ZO258I6CNCN
Resources
[~] AWS::ECS::TaskDefinition NestedMllpStack/MllpServerTask MllpServerTask03D7C754 replace
 └─ [~] ContainerDefinitions (requires replacement)
     └─ @@ -28,10 +28,6 @@
        [ ]   {
        [ ]     "Name": "SENTRY_DSN",
        [ ]     "Value": "https://09874bb720e0f2cd089062e2bb6df994@o4504912808837120.ingest.us.sentry.io/4508855585079297"
        [-]   },
        [-]   {
        [-]     "Name": "RELEASE_SHA",
        [-]     "Value": "1e9cac2a2ae5d671f6d7097bfb3cf44e9f79f756"
        [ ]   }
        [ ] ],
        [ ] "Essential": true,
```

### Testing

- [ ] Merge this

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `040bd5974e4b`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.