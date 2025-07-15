# Some new commands that I just recently learned

## How to release and renew a dhcp obtained IP
```bash
   sudo dhclient -r
   sudo dhclient
```

## How to check and verify the sha256sum
```bash
   sha256sum <file> --check <file.sha256>
 ```

## How to check that fstab is error free
```bash
   sudo mount -a
```

## How to check ports that are open in a linux server
   - Here the flags 
   -- `-i` shows network connections.
   -- `-P` shows port numbers instead of services names.
   -- `-n` shows numerical addresses instead of hostnames.
```bash
   sudo lsof -i -P -n
```
   - Alternatively
   -- `-t` shows tcp ports.
   -- `-u` shows udp ports.
   -- `-l` shows listening ports.
   -- `-n` display numerical addresses.
```bash
   sudo ss -tuln
```

## How to properly use the `/usr` directory
   ### Key Subdirectories in /usr:
       - /usr/bin – Binaries for normal users (e.g., vim, ls, grep).
       - /usr/sbin – System administration binaries (e.g., iptables, fdisk).
       - /usr/lib – Libraries for user applications.
       - /usr/include – Header files for compiling programs.
       - /usr/share – Architecture-independent data (e.g., icons, documentation).
       - /usr/local – For software installed manually (separate from system package manager).

