# Lambda Layer: Lib for Node10-Wrapped PHP7 Apps

This is a simple [Lambda Layer](https://docs.aws.amazon.com/lambda/latest/dg/configuration-layers.html#configuration-layers-manage) for PHP7 apps that use Node10 as a wrapper. It is published in our `nypl-digital-dev` AWS account as [lib-for-node10-wrapped-php7](https://console.aws.amazon.com/lambda/home?region=us-east-1#/layers/lib-for-node10-wrapped-php7/versions/1).

## Usage

To ensure the layer is bound to the Lambda on deploy:

If using `node-lambda`, add the following to your `node-lambda deploy ...` command:
```
 --layers arn:aws:lambda:us-east-1:946183545209:layer:lib-for-node10-wrapped-php7:1
```

To ensure the layer is available when invoking the lambda locally via `sam invoke`:

```
npm install --save-dev NYPL/lib-for-node10-wrapped-php7-lambda-layer#main
```

Then, add the layer as a resource in your `sam` template file as follows:

```
Resources:
  YourService:
    Type: AWS::Serverless::Function
    Properties:
      Handler: index.handler
      ...
      Layers:
      - !Ref LibForPhp7Layer
  LibForPhp7Layer:
    Type: AWS::Serverless::LayerVersion
    Properties:
      LayerName: lib-for-node10-wrapped-php7
      Description:
      ContentUri: node_modules/lib-for-node10-wrapped-php7-lambda-layer/
      CompatibleRuntimes:
      - nodejs10
      LicenseInfo: 'MIT'
      RetentionPolicy: Retain
```
