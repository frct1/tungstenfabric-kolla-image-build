# Kolla's Nova image build recipe with Tungten Fabric driver

Important note: since contrail-vrouter-api is not in dedicated repo we have to install it via template-overrides.j2

```docker
RUN git clone https://github.com/tungstenfabric/tf-controller.git \
    && python3 -m pip install contrail-dev-controller/src/vnsw/contrail-vrouter-api --no-cache-dir install --no-compile \
    && git clone https://github.com/tungstenfabric/tf-nova-vif-driver.git \
    && python3 -m pip install tf-nova-vif-driver --no-cache-dir --no-compile
```

In ideal world we would like to install it via `kolla-build.conf`

First repo contains contrail-vrouter-api library for python (https://github.com/tungstenfabric/tf-controller/tree/master/src/vnsw/contrail-vrouter-api). Somehow it needs to be installed first, may be ordered execution `python3 -m pip --no-cache-dir install /plugins/%plugin_name%` will help.
```
[nova-compute-plugin-contrail-dev-controller]
type = git
location = https://github.com/tungstenfabric/tf-controller 
reference = master

# No way to install nova-vif-driver without contrail-vrouter-api (look above)
[nova-compute-plugin-tf-nova-vif-driver]
type = git
location = https://github.com/tungstenfabric/tf-nova-vif-driver
reference = master
```