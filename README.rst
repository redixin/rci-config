Local config
============

There is a global rally-ci configuration file (config.yaml in this repository).
Items `job` and `script` may be overriden in local config. Local config is file
`.rally-ci.yaml` in project's root.

Sample local configuration::

    ---

    - script:
      name: run_tox
      user: rally
      data: |
        cd /var/repos/$GERRIT_PROJECT
        tox

    - job:
        name: run-tox
        provider: ci4950
        vms:
          - name: u1404_dsvm
          scripts:
            - git_checkout
            - run_tox

Available scripts
-----------------

* git_checkout
  Go to /var/repos/$GERRIT_PROJECTS and check out current patchset.
  This script should be first for any job.

* install_rally
  Install rally in venv and put symlink into /usr/local/bin

* run_scenario
  Run scenario in $RCI_TASK with args $RCI_TASK_ARGS

* stack_sh
  Install devstack.

* create_deployment_devstack
  Create rally deploment from previously installed devstack.

* wait_current_deployment
  Block until cloud is ready.

See config.yaml for more details.
