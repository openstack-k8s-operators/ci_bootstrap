# cifmw_bootstrap

This repo is primarily used to bootstrap the CI environments networking. Given a network layout, networks, subnets, routers and ports will be created and attached to OpenStack instances.

Given the difficulty of testing "trusted" Zuul repo code, this role also supports running outside Zuul against any OpenStack environment. This way patches can be tested without merging code into the repo.

This role can be ran in two ways.

Locally: This will run additional steps to first configure instances and access to them. This will be handled by Zuul node pool in CI but locally we don't have that. After configuring the instances the networking will be configured just like it would be in CI

In CI: In this mode instance creation is completly skipped as instances will be provided to the role from Zuul node pool.

To deploy locally, pass the local tag to do the initial deployment of instances that would be handled by Zuul's `nodepool`:
`ansible-playbook infra-bootstrap.yml -e @my_vars.yml --tags local`

While testing, you may want to skip instance creation after the first deployment, this can by done with the inject tag which will read from the generated inventory file rather than deploying fresh instances.
`ansible-playbook infra-bootstrap.yml -e @my_vars.yml --tags inject`

If you would like to clean up, run infra-bootstrap-cleanup.yml, you can skip cleaning up the network resources with `--skip-tags cleanup_network`:
`ansible-playbook infra-bootstrap-cleanup.yml -e @my_vars.yml --skip-tags cleanup_network --tags inject`

When running in zuul, no tags will be used as that will be the default operation.

Example `my_vars.yml` for local testing:
```
cifmw_bootstrap_router_net: provider_net_shared_3
cifmw_bootstrap_public_key_file: "{{ ansible_user_dir }}/.ssh/id_ed25519.pub"
cifmw_bootstrap_cloud_name: ci_framework
cloud_secrets:
  ci_framework:
    auth_url: "https://openstack.local:13000"
    auth:
      application_credential_id: "<redacted>"
      application_credential_secret: "<redacted>"
    region_name: "regionOne"
    interface: "public"
    identity_api_version: 3
    auth_type: "v3applicationcredential"
zuul:
  build: 1dcaf86e72ec4400a8012f3892d815be
```
