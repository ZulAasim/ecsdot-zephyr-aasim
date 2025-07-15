# ecsdot-zephyr-aasim



## To create custom manifest and use it 

- create a repo with a manifest inside ( west.yml)

This is an example
```
manifest:
  version: "0.12"

  projects:
#    - name: zephyr
#      remote: zephyrproject
#      revision: main
#      path: zephyr

    - name: zephyr
      url: https://github.com/zephyrproject-rtos/zephyr
      revision: zephyr-v3.3.0
      import:
        file: west.yml
        path-prefix: deps
        name-allowlist:
                - cmsis
                - hal_nordic
                - nrfxlib

  self:
    path: app

```

What this does is : uses the manifest found in actual zephyr source code but only
imports the packages written under name-allowlist



## To customise the sdk installation to a specific arch ( Riscv )

```
west sdk install --toolchain riscv64-zephyr-elf
```

