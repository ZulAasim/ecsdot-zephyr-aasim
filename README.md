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

## Zephyr Example Application

Look at the very complete [example-application](https://github.com/zephyrproject-rtos/example-application) !!

## Experimenting with Manifest
```
python3 -m venv ./.venv
source ./.venv/bin/activate

# already installed
# pip install west

west init -m https://github.com/ZulAasim/ecsdot-zephyr-aasim workdir
cd workdir
west update

# no need for these !?
# west zephyr-export
# west packages pip --install
#
# if fresh there is no borked build/
# rm -Rf build/

west build -p -b ganymed_sk/sy120_gbm app/

/root/zephyr-sdk-0.17.2/riscv64-zephyr-elf/bin/riscv64-zephyr-elf-objdump -xsDS build/zephyr/zephyr.elf

/root/zephyr-sdk-0.17.2/riscv64-zephyr-elf/bin/riscv64-zephyr-elf-objdump -xsDS build/zephyr/zephyr.elf > zephyr-elf-dump.s

```


Objdump

**  /root/zephyr-sdk-0.17.2/riscv64-zephyr-elf/bin/riscv64-zephyr-elf-objdump -x -D -S -s   /root/aasim/build/zephyr/zephyr.elf **
