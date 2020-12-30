# import-satellite

The role was created in order to import a mass scale hosts into RedHat Satellite. The role manages hosts that need to connect to different `Content Views` alongside different `Lifecycle Environments`. The role manages these host assignments using customized `Activation Keys` for each one of the hosts types.

An `Activation Key` is assigned to a host using a combination of it's `Lifecycle Environment` variable that is defined by the group that the host is a part of
