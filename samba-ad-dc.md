# Commands for Samba Active Directory Domain Controller

## How to execute a command specifying a particular user

   ```bash
   samba-tool dns serverinfo $(hostname -f) -U Administrator
   ```

## How to check Kerberos ticket status

   ```bash
   klist
   ```

## How to resolve a samba ad dc server from a linux host
   ```bash
   sudo vim /etc/systemd/resolved.conf
   ```
   - Then add the following lines:
   ```vim
   [Resolve]
   DNS=<SAMBA-AD-DC-IP> 8.8.8.8
   Domanis=yourdomain.example
   ```
   - Then restart and verify the resolution
   ```bash
   sudo systemctl restart systemd-resolved
   resolvectl status
   nslookup yourdomain.example
   ```

## How to join a computer to a domain
   - If the host computer is Linux with a Debian based system you first need:
   ```bash
   sudo apt update
   sudo apt install realmd sssd sssd-tools libnss-sss libpam-sss adcli samba-common-bin oddjob oddjob-mkhomedir packagekit krb5-user
   ```
   - The join by
   ```bash
   sudo realm join -v --membership-software=samba --client-software=winbind  yourdomain.example
   ```
   - Enable manual login by lightdm
   ```bash
   sudo vim /etc/lightdm/lightdm.conf
   ```
   - Add the following lines
   ```ini
   [Seat:*]
   greeter-show-manual-login=true
   greeter-hide-users=true
   ```
   - Restart lightdm
   ```bash
   sudo systemctl restart lightdm
   ```

## How to create a home dir and login shell for a new user when login into a joined computer
   - First execute
   ```bash
   sudo pam-auth-update --enable mkhomedir
   ```
   - Then for Debian based systems add the following line to `/etc/pam.d/common-session`:
   ```bash
   session optional        pam_mkhomedir.so skel=/etc/skel umask=077
   ```

## How to omit the fully qualified domain name when login as user
   - First you need to modify `/etc/sssd/sssd.conf`
   ```ini
   [domain/yourdomain.example]
   use_fully_qualified_names = False
   fallback_homedir = /home/%u
   ```
   - Then restart
   ```bash
   sudo systemctl restart sssd
   ```

## How to list users with a full qualified domain name

   ```bash
   sudo samba-tool user list --full-dn
   ```

## How to create an OU in samba AD DC

   ```bash
   sudo samba-tool ou create "OU=OU_NAME"
   ```

## How to fix deprecation of arcfour-hmac encryption type
   - Edit the file `/etc/krb5/krb5.conf` or `/etc/krb5.conf`
   ```ini
   [libdefaults]
   default_realm = YOUR.REALM.COM
   permitted_enctypes = aes256-cts-hmac-sha1-96 aes128-cts-hmac-sha1-96
   default_tgs_enctypes = aes256-cts-hmac-sha1-96 aes128-cts-hmac-sha1-96
   default_tkt_enctypes = aes256-cts-hmac-sha1-96 aes128-cts-hmac-sha1-96
   allow_weak_crypto = false
   ```
   - Ensure active directory user supports thos encryption types. Go to Active Directory Users and Computers -> User's properties and account tab and check:
      - [x] This account supports Kerberos AES 128 bit encryption
      - [x] This account supports Kerberos AES 256 bit encryption
   
