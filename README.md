# CDK-Stuff

Layer 1: CFN Constructs
Direct CloudFormation resources. These are low-level constructs that map directly to AWS CloudFormation resources. They give you the most control but require more detailed configuration.

Prefix: Cfn (e.g., CfnBucket, CfnVpc).
Use case: When you need to use a feature not yet abstracted by CDK or need fine-grained control.

  from aws_cdk import aws_s3 as s3
  from aws_cdk import Stack
  from constructs import Construct
  
  class Layer1Stack(Stack):
      def __init__(self, scope: Construct, id: str, **kwargs):
          super().__init__(scope, id, **kwargs)
  
          s3.CfnBucket(
              self,
              "MyCfnBucket",
              bucket_name="my-layer1-bucket"
          )

Layer 2: AWS Construct Library
AWS abstractions. These are higher-level constructs that abstract common AWS resource configurations. They simplify usage by providing sensible defaults and convenience methods.

Prefix: No specific prefix (e.g., Bucket, Vpc).
Use case: When you want to define AWS resources with a simplified API and default configurations.

  from aws_cdk import aws_s3 as s3
  from aws_cdk import Stack
  from constructs import Construct
  
  class Layer2Stack(Stack):
      def __init__(self, scope: Construct, id: str, **kwargs):
          super().__init__(scope, id, **kwargs)
  
          bucket = s3.Bucket(
              self,
              "MyBucket",
              bucket_name="my-layer2-bucket",
              versioned=True
          )


Layer 3: Patterns
High-level constructs for common patterns. These are pre-configured, opinionated constructs that combine multiple resources to implement specific use cases or architectural patterns.

Namespace: aws_cdk_patterns or similar.
Use case: When you want to deploy a complete solution (e.g., API Gateway with Lambda or a VPC with subnets).

  from aws_cdk.aws_apigatewayv2_alpha import HttpApi
  from aws_cdk import Stack
  from constructs import Construct
  
  class Layer3Stack(Stack):
      def __init__(self, scope: Construct, id: str, **kwargs):
          super().__init__(scope, id, **kwargs)
  
          # Example: Deploy an HTTP API
          api = HttpApi(
              self,
              "MyHttpApi",
              description="Layer 3 HTTP API with sensible defaults"
          )


Summary of CDK Layers
Layer	Description	Example	When to Use
Layer 1	Raw CloudFormation resources. Most control but verbose.	CfnBucket	For advanced configurations or features not supported in Layer 2 or Layer 3.
Layer 2	Simplified AWS resources with built-in defaults and methods.	Bucket, Vpc	For most use cases where you need AWS resources with less boilerplate.
Layer 3	High-level patterns for common architectures. Combines multiple Layer 2 constructs.	HttpApi, ApplicationLoadBalancedFargateService	For quickly deploying full solutions using best practices.



