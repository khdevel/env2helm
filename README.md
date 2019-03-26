# What

Allows you to change and populate Helm Values file (or any yaml file for that matter), using env variables. The `ironhalik/env2helm` docker image comes with latest-ish Helm and kubectl for your convenience.

# How

Example *values.yaml*:  
```yaml
image:  
  repository: alpine  
  tag: 3.9
```

```console
$ export HELM_IMAGE_REPOSITORY=ubuntu  
$ export HELM_IMAGE_TAG=bionic  
$ env2helm -f values.yaml
```

will output:
```yaml
image:
  repository: ubuntu
  tag: bionic
```
If you're using it in a CI environment, you can use `-i` or `--in-place` flag to overwrite the input files with any changes. Alternatively, depending on your shell, you can do something along the lines of `helm install -f <(env2helm -f some-values-file.yaml)`

# Usage
```
usage: env2helm [-h] -f FILES [-p PREFIX] [--in-place] [--strict]

Map ENV vars to yaml

optional arguments:
  -h, --help            show this help message and exit

required arguments:
  -f FILES, --file FILES
                        Files to process. Can be supplied multiple times.

optional arguments:
  -p PREFIX, --prefix PREFIX
                        Prefix to look for in env variables. Defaults to HELM
  -i, --in-place        Overwrite files instead of printing to stdout. Think
                        sed -i
  --strict              Exit with non-zero status code when an env var didnt
                        match any yaml value
```
