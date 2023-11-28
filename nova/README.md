# Kolla's Nova image build recipe with Tungten Fabric driver
In ideal world we would like to install it via `kolla-build.conf`

## ⚠️ kolla-build.conf for nova is not tested yet. read below

Due to recent move vrouter-api lib to dedicated repo it was not tested. tf-nova-vif-driver is depends from vrouter-api. Not sure how to organize ordered installation of plugins.

First repo contains contrail-vrouter-api library for python (https://github.com/tungstenfabric/tf-controller/tree/master/src/vnsw/contrail-vrouter-api). Somehow it needs to be installed first, may be ordered execution `python3 -m pip --no-cache-dir install /plugins/%plugin_name%` will help.

Your kolla-build.conf will look like that:
```
[nova-compute-plugin-tf-vrouter-api]
type = git
location = https://github.com/baikov-ilia/tf-vrouter-api
reference = master

# No way to install nova-vif-driver without contrail-vrouter-api (look above)
[nova-compute-plugin-tf-nova-vif-driver]
type = git
location = https://github.com/tungstenfabric/tf-nova-vif-driver
reference = master
```
tf-vrouter-api has been placed to separated [baikov-ilia/tf-vrouter-api](https://github.com/baikov-ilia/tf-vrouter-api) in order to make it compatible with kolla-build.conf. Regarding [kolla-build plugin section](https://docs.openstack.org/kolla/latest/admin/image-building.html#plugin-functionality) it is not a best way to add plugins with `template-overrides.j2`
