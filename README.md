# Tungsten Fabric kolla image build
This repo describes on how to build Nova and Neutron images contains TungstenFabric using vanilla kolla build tools.

# Building it up
_Firstly please take a look to_ [kolla-build docs](https://docs.openstack.org/kolla/latest/admin/image-building.html)

Once you are ready navigate to `neutron` or `nova` directory and run
```console
kolla-build -b ubuntu ^nova-compute$ --config-file kolla-build.conf --template-override template-overrides.j2
```
and wait until build is finished. Example for `nova-compute` image. In case of neutron it should be `^neutron-server$`.

## TungstenFabric community in Telegram
[![TungstenFabric Telegram Community](tf_logo.png)](https://t.me/tungstenfabric_ru)