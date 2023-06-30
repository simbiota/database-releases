# Database releases for SIMBIoTA

Download your selected database release from the releases of this repository.
```bash
curl https://github.com/simbiota/database-releases/releases/download/20230630/simbiota-arm-20230630.sdb -o /var/lib/simbiota/simbiota-arm-20230630.sdb
```
Configure Simbiota to use this database by setting the `database.database_file` key in your config.
```
# /etc/simbiota/client.yaml
---
...
database:
  database_file: /var/lib/simbiota/simbiota-arm-20230630.sdb
...
```

## Details

We plan to regularly release databases that SIMBIoTA can use for detection.
The databases are currently divided by the target architecture of the samples.
We know that this is not the best solution because an architecture is used by a range of devices that run incompatible binaries because of library, kernel etc. differences.
For example most Android devices and IoT devices run some version of ARM but most Android malware won't be able to run on other IoT devices, and the other way around.
Another thing is that ARMv7 (32 bit) binaries will only run on devices with supporting 32-bit libraries installed.
Another thing is emulation and compatibility layers that enable execution of programs written for different platforms ([`wine`](https://www.winehq.org)) or architectures ([`qemu`](https://www.qemu.org/)).
And so malicious programs written for different platforms may still be seemlessly executed for example through [`binfmt`](https://www.freedesktop.org/software/systemd/man/binfmt.d.html#).

This means that currently there will be many objects in the database that provide detection for malware that wouldn't run on your device so detecting these is not necessary.
So databases are a bit _"bloated"_ at this point (`~4MB` for ARM).
We plan to support so called _platforms_ that are a combination of architecture, kernel, library etc. versions and so provide a more granular approach towards specifying malware samples that should be included in a database.