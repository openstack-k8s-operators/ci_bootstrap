To deploy locally, pass the local tag to do the inital configuration:

`ansible-playbook infra-bootstrap.yml --tags local -e @my_vars.yml`

While testing, you may want to skip instance creation, this can by done with the inject tag which will read from the inventory file rather than deploying fresh instances.
`ansible-playbook infra-bootstrap.yml --tags inject -e @my_vars.yml`

If you would like to clean up, run infra-bootstrap-cleanup.yml, you can skip cleaning up the network with `--skip-tags cleanup_network:`
`ansible-playbook infra-bootstrap-cleanup.yml -e @my_vars.yml --skip-tags cleanup_network`
