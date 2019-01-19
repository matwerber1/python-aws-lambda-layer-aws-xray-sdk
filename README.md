# Pre-Requisites

Python and pip 3.7 is installed.

# Instructions

1. Install aws-xray-sdk locally, upload it as a zip to S3, and create a lambda layer
```sh
S3_BUCKET='<YOUR_BUCKET>'

pip3.7 install aws-xray-sdk -t ./python

zip -r layer.zip ./python

aws s3 cp layer.zip s3://$S3_BUCKET/layer.zip

aws lambda publish-layer-version \
  --layer-name python37-aws-xray-sdk \
  --compatible-runtimes python3.7 \
  --content S3Bucket=$S3_BUCKET,S3Key=layer.zip
  
```

2. Associate your Lambda function with your newly created Lambda Layer. 

3. [Instrument your Lambda function to use the xray SDK](https://docs.aws.amazon.com/lambda/latest/dg/python-tracing.html).