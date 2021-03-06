import-satellite
================

The role was created in order to import a mass scale hosts into RedHat Satellite. The role manages hosts that need to connect to different `Content Views` alongside different `Lifecycle Environments`. The role manages these host assignments using customized `Activation Keys` for each one of the hosts types.

An `Activation Key` is assigned to a host using a combination of it's `Lifecycle Environment` variable that is defined by the group that the host is a part of, and it's `OS Version` which is pulled using the `gather_facts` ansible module. The version of the operating system corresponds with the `Content View` in Red Hat Satellite.

The `Lifecycle Environments` used in the role -
- dev
- local-prod
- customer-prod

The RHEL versions that the role supports -
- 7.4
- 7.6
- 7.8
- 7.9

Prerequisites
-------------

The role relies on a community based `ansible module`. Make sure to install it before running the role.
```
ansible-galaxy collection install community.general
```

Parameters
---------
- **Variable:** `satellite_url`.
  - Description: the base url of the Satellite server.
  - Default value: http://10.35.97.198
  - Default definition: the variable is defined at `roles/import-satellite/defaults/main.yml` and can be overwritten to fit any other environment.
  - **Note:** **the environment can be modifies and changed**

- **Variable:** `organization_id`.
  - Description: the base organization ID in the Satellite server.
  - Default value: Cool-Organization
  - Default definition: the variable is defined at `roles/import-satellite/defaults/main.yml` and can be overwritten to fit any other environment.
  - **Note:** **the environment can be modifies and changed**
  
- **Variable:** `satellite_tools_repository`.
  - Description: the name of the Satellite Tools repository.
  - Default value: rhel-7-server-satellite-tools-6.8-rpms
  - Default definition: the variable is defined at `roles/import-satellite/defaults/main.yml`.
  - **Note:** **Do not change unless required**
  
- **Variable:** `katello_package_name`.
  - Description: the name of the Satellite Tools package.
  - Default value: katello-host-tools
  - Default definition: the variable is defined at `roles/import-satellite/defaults/main.yml`.
  - **Note:** **Do not change unless required**
  
- **Variables:** `rhel7.<4|6|8|9>-<dev|local-prod|customer-prod>`.
  - Description: Multiple variable that define how an `Activation Key` should look like. Each value is a different `Activation Key`.
  - Default value: **Not Consistent** Relys on the key value from Satellite.
  - Default definition: the variable is defined at `group_vars/<dev|local-prod|customer-prod>/key.yml`.
  - **Note:** **Mandatory Variable that must be applied**

- **Variable:** `env`.
 - Description: the name of the environment to which the server should be registered to.
 - Default value: <none> - parameter is mandatory.
 - Default definition: the variable is defined per ansible group at `group_vars/<dev|local-prod|customer-prod>/key.yml`.
 - **Note:** **Mandatory Variable that must be applied**

Inventory
---------

- Description: The inventory is defined in the `./invenotry` file. The inventory is seperated into 3 groups - `dev|local-prod|customer-prod`, each server that is added into the inventory file should be under the correct group.
- **Note:** **Make sure that the correct authentication method is implemented, and that the servers are reachable**
- Default value:
```
[dev]
server-a.ocp.lab ansible_user=root

[local-prod]
server-b.ocp.lab ansible_user=root

[customer-prod]
server-c.ocp.lab ansible_user=root
```

Running the Role
----------------

To run the role, invoke the playbook that is present in the repository.
```
ansible-playbook -i inventory import-servers
```
