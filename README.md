# aws-panw-vmseries-cft-deployment
Various CFT-based solutions are collected in this repository for puposes of deploying Software Firewall labs in the context of AWS events platform. Most recently used as AWS Re:invent 2023.

## Outline

### [vmseries-gwlb-2023](https://github.com/seanyoungberg/panw-vmseries-aws-jam/tree/main/vmseries-gwlb-2023)

This is the version being used for Re:invent Jam 2023. It is structured in a specific way to meet the layout of the Jam Event platform.

- aws-jam-panw-gwlb-cfn-root.yaml. This is the root stack that will be deployed. The other template files are nested from this one.

To deploy in normal AWS account:

1. Prep S3 bucket

Jam will use bucket names `aws-jam-challenge-resources-us-east-1`

To deploy in a separate account, prepare a bucket with same format but apply a unique prefix to the bucket. For example, we used `panw-aws-jam-challenge-resources-us-east-1`

2. Upload assets to S3


- The nested templates (combined, security, vmseries)
- authcodes
- bootstrap.xml
- init-cfg.txt

The JAM platform doesn't have support for folders in the S3 bucket, so we will do the same here and drop everyting in root of the bucket. Script in the CFT will be used to acutally generate the bootsrap bucket using these assets in the appropriate format.

3. Deploy stack

Use aws-jam-panw-gwlb-cfn-root.yaml to create the stack. There is only one parameter that will need to be modified, which is the name of the bucket. Modify the bucket to include the prefix used in your account
