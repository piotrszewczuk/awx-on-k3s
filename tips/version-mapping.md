<!-- omit in toc -->
# Version Mapping between AWX Operator and AWX

- [Default version mapping betwern AWX Operator and AWX](#default-version-mapping-betwern-awx-operator-and-awx)
- [Appendix: Gather bundled AWX version from AWX Operator](#appendix-gather-bundled-awx-version-from-awx-operator)

## Default version mapping betwern AWX Operator and AWX

The table below maps the AWX Operator versions and bundled AWX versions.

| AWX Operator | AWX |
| - | - |
| 0.22.0 | 21.1.0 |
| 0.21.0 | 21.0.0 |
| 0.20.2 | 21.0.0 |
| 0.20.1 | 21.0.0 |
| 0.20.0 | 20.1.0 |
| 0.19.0 | 20.0.1 |
| 0.18.0 | 20.0.1 |
| 0.17.0 | 20.0.0 |
| 0.16.1 | 19.5.1 |
| 0.16.0 | 19.5.1 |
| 0.15.0 | 19.5.0 |
| 0.14.0 | 19.4.0 |
| 0.13.0 | 19.3.0 |
| 0.12.0 | 19.2.2 |
| 0.11.0 | 19.2.1 |
| 0.10.0 | 19.2.0 |
| 0.9.0 | 19.1.0 |
| 0.8.0 | 19.0.0 |
| 0.7.0 | 18.0.0 |
| 0.6.0 | 15.0.0 |

In the current version of AWX Operator, [there is `image_version` parameter for AWX resource to change which image will be used](https://github.com/ansible/awx-operator#deploying-a-specific-version-of-awx), but it appears that using a version of AWX other than the one bundled with the AWX Operator [is currently not supported](https://github.com/ansible/awx-operator#deploying-a-specific-version-of-awx).

## Appendix: Gather bundled AWX version from AWX Operator

- For AWX Operator **0.15.0 or later**

  ```bash
  # Using Docker
  docker run -it --rm --entrypoint /usr/bin/bash quay.io/ansible/awx-operator:${OPERATOR_VERSION} -c env | grep DEFAULT_AWX_VERSION

  # Using Kubernetes
  kubectl run awx-operator --restart=Never -it --rm --command /usr/bin/bash --image=quay.io/ansible/awx-operator:${OPERATOR_VERSION} -- -c "env" | grep DEFAULT_AWX_VERSION
  ```

- For AWX Operator **0.10.0 to 0.14.0**

  ```bash
  curl -sf https://raw.githubusercontent.com/ansible/awx-operator/${OPERATOR_VERSION}/roles/installer/defaults/main.yml | egrep "^image_version:"
  ```

- For AWX Operator **0.9.0**

  ```bash
  curl -sf https://raw.githubusercontent.com/ansible/awx-operator/${OPERATOR_VERSION}/roles/installer/defaults/main.yml | egrep "^tower_image_version:"
  ```

- For AWX Operator **0.7.0 and 0.8.0**

  ```bash
  curl -sf https://raw.githubusercontent.com/ansible/awx-operator/${OPERATOR_VERSION}/roles/installer/defaults/main.yml | egrep "^tower_image:"
  ```

- For AWX Operator **0.6.0**

  ```bash
  curl -sf https://raw.githubusercontent.com/ansible/awx-operator/${OPERATOR_VERSION}/roles/awx/defaults/main.yml | egrep "^tower_image:"
  ```
