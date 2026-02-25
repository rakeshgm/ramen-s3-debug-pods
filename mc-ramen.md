# mc Commands – S3 Debug Pod

## Change the namespace of the s3-debug pod

- Make sure the pod runs in the **same namespace as the Ramen pods**
- By default, the pod definition uses `openshift-dr-system`
- If Ramen is running in a different namespace, update the `namespace` field in the pod YAML accordingly

## Enter the Pod

```sh
oc exec -it -n openshift-dr-system s3-debug -- /bin/sh
```

---

## Configure S3 Alias

```sh
mc alias set s3 https://<endpoint> <ACCESS_KEY> <SECRET_KEY>
```

Verify alias:

```sh
mc alias list
```

---

## List Buckets

```sh
mc ls s3
```

---

## List Objects in a Bucket

```sh
mc ls s3/<bucket-name>
```

Recursive listing:

```sh
mc ls --recursive s3/<bucket-name>
```

---

## Upload a File (Write Test)

```sh
echo "hello from s3-debug pod" > /tmp/hello.txt
mc cp /tmp/hello.txt s3/<bucket-name>/hello.txt
```

---

## Read an Object

```sh
mc cat s3/<bucket-name>/hello.txt
```

---

## Download an Object

```sh
mc cp s3/<bucket-name>/hello.txt /tmp/hello.txt
```

---

## Object Metadata

```sh
mc stat s3/<bucket-name>/<object-name>
```

> Note: `mc stat` works on objects, not buckets.

---

## Delete an Object

```sh
mc rm s3/<bucket-name>/<object-name>
```

---

## Common Errors

- `CERTIFICATE_VERIFY_FAILED` → CA trust issue
- `AccessDenied` → bucket or credentials are read-only
- `mkdir /.mc: permission denied` → `$HOME` not writable
