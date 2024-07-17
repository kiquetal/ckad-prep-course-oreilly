### Resource Requests

- spec.containers[].resources.requests
- Resources types include CPU,memory, huge page, ephermal storage

### Notes

| YAML | Description | Example |
| ---- | ----------- | ------- |
|spec.containers[].resources.requests.cpu | CPU resource type | 500m|
|spec.containers[].resources.requests.memory | Memory resource type | 64Mi |
| spec.containers[].resources.requests.hugepages-<size> | Huge page resource type | hugepages-2Mi: 60Mi |
| spec.containers[].resources.requests.ephemeral-storage | Ephemeral storage type | 4Gi |
