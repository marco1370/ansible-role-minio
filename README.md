# ansible-role-minio
Ansible role for deploying the MinIO binary and configure it

## How to install
### requirements.yml
**Put the file in your roles directory**
```yaml
---
- src: https://github.com/mohsenmirzaei1991/ansible-role-minio.git
  scm: git
  version: main
  name: ansible-role-minio
```
### Download the role
```Shell
ansible-galaxy install -f -r ./roles/requirements.yml --roles-path=./roles
```

## Requirements

- Ansible >= 2.10 **(No tests has been realized before this version)**

## Role Variables

All variables which can be overridden are stored in [default/main.yml](default/main.yml) file as well as in table below.

| Name           | Default Value | Choices | Description                        |
| -------------- | ------------- | ------- | -----------------------------------|
| `minio_version` | "latest" | [version](https://github.com/minio/minio/tags) | Choice of the minio version. |
| `minio_root_user` | "minioadmin" |  | MinIO root user |
| `minio_root_password` | "minioadmin" |  | MinIO root password |
| `minio_opts` | "[]" |  |  |
| `minio_enable_browser` | "true" | true / false |  |
| `minio_server_url` | "[]" | An URL | URL to access the server |
| `minio_extra_env` | "[]" |  | Some ENV variables for MinIO |
| `minio_storage_dir` | "/var/minio" |  | MinIO storage dir |
| `minio_certs_dir` | "/etc/ssl/minio/" |  | MinIO SSL storage dir |

## Example Playbook

```yaml
---
- hosts: all
  tasks:
    - name: Include ansible-role-minio
      include_role:
        name: ansible-role-minio
      vars:
        minio_version: 'RELEASE.2021-12-20T22-07-16Z'
        minio_opts:
          - --certs-dir {{ minio_certs_dir }}
          - --console-address :8443
          - --quiet
          - --anonymous
```
