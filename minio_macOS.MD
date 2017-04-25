
# Minio Installation on macOS

## Fresh Install

Install Minio packages for macOS via brew.

```
brew install minio/stable/minio
minio server ~/Photos
```

## Upgrade 

Step 1: Uninstall minio if you installed it using `brew install minio`

```
brew uninstall minio 
```
Step 2: Fresh Install using new path

Once you remove minio completely from your system, proceed to do :

```
brew install minio/stable/minio
```

## Important Breaking Change

> The command `brew upgrade minio` will no longer work

Minio does not work with go1.8 because of upstream bugs in golang such as https://github.com/golang/go/issues/19734 which are addressed in go1.8.1

We will re-enable minio installation on macOS via `brew install minio` once we evaluate these fixes in go 1.8.1 version.
