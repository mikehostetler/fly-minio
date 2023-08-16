# fly-minio

This repo contains a template to run [Minio](https://min.io/) on [Fly.io](https://fly.io/) using the Apps V2 platform.  The Minio machine scales to zero and wakes up upon access.

## Deploy

To host uptime kuma on Fly.io clone this repo, enter the folder and run:

```
fly launch \
  --copy-config \
  --no-public-ips \
  --no-deploy \
  --ha=false

fly secrets set \
  MINIO_ROOT_USER=minioroot \ 
  MINIO_ROOT_PASSWORD=miniosecretpassword

fly deploy
```

You will be asked an app name and organization. A 1GB volume will be created on deploy.


## Create a Bucket Alias

Use the Minio Console to create a bucket alias. The alias will be used to access the bucket via the fly.io domain.

```
mc config host add fly-minio http://<YOUR-APP>.fly.dev:9000 minioroot miniosecretpassword
```


## Create a public bucket

```
mc mb fly-minio/public-bucket

mc anonymous set download fly-minio/public-bucket
```

## List files in your bucket

```
mc ls fly-minio
```


## Feedback?

https://community.fly.io/ ...TODO

## Wishlist

I'd love to scale this out to a High Availability solution using Minio clustering across multiple regions on Fly. If you have any ideas on how to do this, please let me know! PR's welcome!