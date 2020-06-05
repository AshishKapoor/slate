# Cloud Buckets

The client can share their data to be read by Rill. 

## Google Cloud 

For sharing any Google Storage Bucket from a specific Google Cloud Project, we need to provide access to the Rill GCP Service Account (GSA).

This Service Account is specific to the workspace and does NOT share credentials with any other workspaces. 

The Service Account can be retrieved from the Rill Control Center. They are generally in format of

`${organization}@iam.rilldata.com`

### To provide access using CLI
```shell
$ gsutil defacl ch -u \
    ${organization}@iam.rilldata.com:OWNER \
    gs://${BUCKET}
```
### To provide access using Console

* Go to Storage Console: https://console.cloud.google.com/storage/browser.
* Select the bucket we want to provide access to.
* Select Permissions tab.
* Add permissions.

![](../images/1.png?raw=true)


### References
* https://cloud.google.com/dataprep/docs/concepts/gcs-buckets#granting_service_account_access_to_a_bucket

## Amazon Web Services

We can provide access to the S3 Bucket through an IAM Role which will be assumed by the Rill Data AWS Account to gain the access to the buckets. 

### Create Role using Cloudformation Console

> Use the following Cloudformation Template.

```yaml
AWSTemplateFormatVersion: '2010-09-09'
Metadata:
  License: Apache-2.0

Description: 'AWS CloudFormation Template for providing Rill Data Access to S3 Bucket. It creates a
  Role that can be assumed by the RillData AWS Account. The Role has a IAM policy associated with them.'

Parameters:
  BucketName:
    Type: String
    Description: S3 Bucket Name. Don't append s3://.
  NamePrefix:
    Type: String
    Description: Name prefix for the IAM Policy and IAM Role.
    Default: rilldata
  ExternalID:
    Type: String
    Description: External ID for Secured Cross Account Access.
    Default: r!lld@ta

Resources:
  S3Role:
    Type: AWS::IAM::Role
    Properties:
      Description: 'RillData Access to the S3 Bucket. Managed by: Cloudformation'
      AssumeRolePolicyDocument:
        Version: '2012-10-17'
        Statement:
          - Effect: Allow
            Principal:
              AWS:
                - 'arn:aws:iam::248432388601:root'
            Action:
              - 'sts:AssumeRole'
            Condition:
              StringEquals:
                'sts:ExternalId': !Ref ExternalID
      Policies:
        - PolicyName: !Join
            - ''
            - - !Ref NamePrefix
              - 'S3AccessPolicy'
          PolicyDocument:
            Statement:
            - Effect: Allow
              Action: ['s3:*']
              Resource:
                - !Join
                  - ''
                  - - 'arn:aws:s3:::'
                    - !Ref BucketName
                - !Join
                  - ''
                  - - 'arn:aws:s3:::'
                    - !Ref BucketName
                    - '/*'
      RoleName: !Join
        - '-'
        - - !Ref NamePrefix
          - s3-access
      Tags:
        - Key: Accessor
          Value: RillData
        - Key: ManagedBy
          Value: Cloudformation

Outputs:
  RoleName:
    Value: !GetAtt [S3Role, Arn]
    Description: S3 Access Role Arn, to be shared with RillData
  ExternalID:
    Value: !Ref ExternalID
    Description: ExternalID for Secured Access, to be shared with RillData
```

* Open AWS Cloudformation to create a new Stack - https://console.aws.amazon.com/cloudformation/home?region=us-east-1#/stacks/create/template
* Upload the CFN Template and Specify Stack details.
** Stack Name: `rilldata-s3-access`
** Bucket Name: Name of the bucket we want to provide access to.

![](../images/2.png?raw=true)

* Click Next, Again Next, Acknowledge the Capabilities and Create the Stack.
* You can check the events and it should create the resources for you.

![](../images/3.png?raw=true)

* Share the Outputs with Rill Data

![](../images/4.png?raw=true)