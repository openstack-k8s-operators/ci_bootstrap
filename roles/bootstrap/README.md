# bootstrap
The bootstrap role assists on creating cloud resources needed to deploy Red Hat OpenStack Services on OpenShift.
It supports OpenStack cloud as provider.

## Parameters
* `cifmw_bootstrap_network_default_router_net`: (String) Name of the network to be used an external gateway. Defaults to: `public`.
* `cifmw_bootstrap_openstack_config_dir`: (String) Path to the openstack config directory for clouds.yaml. Defaults to `"{{ ansible_user_dir }}/.config/openstack"`.
* `cifmw_bootstrap_clouds_yaml`: (String) Path to the clouds.yaml for provider's access. Defaults to `"{{ cifmw_bootstrap_openstack_config_dir }}/clouds.yaml"`.
* `cifmw_bootstrap_openstack_cmd_retries_value`: (Integer) Default number os retries when running some openstack commands. Defaults to `10`.
* `cifmw_bootstrap_openstack_cmd_delay_value`: (Integer) Default delay value when retrying some openstack commands. Defaults to `5`.
* `cifmw_bootstrap_ci_infra_dir`: (String) Directory where to search and save CI environment files. Default to `"/etc/ci/env"`.
* `cifmw_bootstrap_net_env_def_path`: (String) Path to the network environment definition file. Defaults to `"{{ cifmw_bootstrap_ci_infra_dir }}/networking-environment-definition.yml"`
* `cifmw_bootstrap_create_application_credential`: (Boolean) Whether to create application credentials and use them for all subsequent OpenStack operations. Defaults to `false`.

## TODO
* Management of computes resources is not yet supported.