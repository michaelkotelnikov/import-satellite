import-satellite
================

The role was created in order to import a mass scale hosts into RedHat Satellite. The role manages hosts that need to connect to different `Content Views` alongside different `Lifecycle Environments`. The role manages these host assignments using customized `Activation Keys` for each one of the hosts types.

An `Activation Key` is assigned to a host using a combination of it's `Lifecycle Environment` variable that is defined by the group that the host is a part of, and it's `OS Version` which is pulled using the `gather_facts` ansible module. The version of the operating system corresponds with the `Content View` in Red Hat Satellite.

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
