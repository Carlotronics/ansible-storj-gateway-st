# Storj gateway-st

This role aims to deploy Storj [single-tenant
gateway](https://github.com/storj/gateway-st/) on a given host. 

Storj gateway-st is a S3 gateway to the Storj network.

## Usage

Add these lines to your `requirements.yml`:
```yaml
roles:
  - name: phowork.storj-gateway-st
    src: git+https://gitlab.phowork.fr/phowork/iac/ansible/roles/storj-gateway-st.git
    version: 0.1.0
```

Example of playbook, with its associated variables file:
```yaml
---

- hosts: all
  roles:
    - {role: phowork.storj-gateway-st, tags: ['gateway-st']}
```

Variables file:
```yaml
storj_gateway_st_version: "1.5.1"

# StorJ Gateway ST configuration keys
storj_gateway_st_minio_access_key: "<THE S3 ACCESS KEY YOU'LL USE>"
storj_gateway_st_minio_secret_key: "<THE S3 SECRET KEY YOU'LL USE>"
storj_gateway_st_access: "<STORJ ACCESS GRANT>"
storj_gateway_st_server_address: 127.0.0.1:7777
storj_gateway_st_tracing_enabled: "true"
storj_gateway_st_tracing_interval: 30s
storj_gateway_st_tracing_sample: 0.1
storj_gateway_st_website: "false"
storj_gateway_st_log_level: info
storj_gateway_st_log_output: "{{ storj_gateway_st_path }}/logs/gateway-st.log"
storj_gateway_st_log_stack: "false"

# Some optional additional options
storj_gateway_st_additional_options:
  - key: s3.disable-copy-object
    value: "true"
  - key: metrics.interval
    value: 1m0s
```
