## S3 Debug Pod – aws-cli (OpenShift / Ramen)

Purpose

Use this pod to debug S3 access using aws-cli in the same environment where
Ramen (ODR) runs. This helps verify TLS, CA trust, and read/write permissions.

## Enter the Pod

``` sh
oc exec -it -n openshift-dr-system awscli-debug -- /bin/sh
```

### Configure AWS Credentials

```sh
aws configure
```

Provide:

```
Access Key
Secret Key
Region (any value, e.g. us-east-1)
Output format (optional)
```

- Credentials are stored in `$HOME/.aws/`

### List Buckets

```sh
aws s3 ls --endpoint-url https://<endpoint>
```

### List Objects in a Bucket

```sh
aws s3 ls s3://<bucket-name> --endpoint-url https://<endpoint>
```

### Recursive

```sh
aws s3 ls s3://<bucket-name> --recursive --endpoint-url https://<endpoint>
```

### Upload an Object (Write Test)

```sh
echo "hello from aws-cli" > /tmp/hello.txt
```

``` sh
aws s3 cp /tmp/hello.txt s3://<bucket-name>/hello.txt --endpoint-url https://<endpoint>
```

### Read / Download an Object: Print to stdout

```sh
aws s3 cp s3://<bucket-name>/hello.txt - --endpoint-url https://<endpoint>
```

### Download to file

```sh
aws s3 cp s3://<bucket-name>/hello.txt /tmp/hello.txt --endpoint-url https://<endpoint>
```
