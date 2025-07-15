# Commands for Samba Active Directory Domain Controller

## How to execute a command specifying a particular user

   @code bash
   samba-tool dns serverinfo $(hostname -f) -U Administrator
   @end

## How to check Kerberos ticket status

   @code bash
   klist
   @end

## How to resolve a samba ad dc server from a linux host
   @code bash
   sudo vim /etc/systemd/resolved.conf
   @end
   - Then add the following lines:
   @code vim
   [Resolve]
   DNS=<SAMBA-AD-DC-IP> 8.8.8.8
   Domanis=yourdomain.example
   @end
   - Then restart and verify the resolution
   @code bash
   sudo systemctl restart systemd-resolved
   resolvectl status
   nslookup yourdomain.example
   @end

## How to join a computer to a domain
   - If the host computer is Linux with a Debian based system you first need:
   @code bash
   sudo apt update
   sudo apt install realmd sssd sssd-tools libnss-sss libpam-sss adcli samba-common-bin oddjob oddjob-mkhomedir packagekit krb5-user
   @end
   - The join by
   @code bash
   sudo realm join -v --membership-software=samba --client-software=winbind  yourdomain.example
   @end
   - Enable manual login by lightdm
   @code bash
   sudo vim /etc/lightdm/lightdm.conf
   @end
   - Add the following lines
   @code ini
   [Seat:*]
   greeter-show-manual-login=true
   greeter-hide-users=true
   @end
   - Restart lightdm
   @code bash
   sudo systemctl restart lightdm
   @end

## How to create a home dir and login shell for a new user when login into a joined computer
   - First execute
   @code bash
   sudo pam-auth-update --enable mkhomedir
   @end
   - Then for Debian based systems add the following line to `/etc/pam.d/common-session`:
   @code bash
   session optional        pam_mkhomedir.so skel=/etc/skel umask=077
   @end

## How to omit the fully qualified domain name when login as user
   - First you need to modify `/etc/sssd/sssd.conf`
   @code ini
   [domain/yourdomain.example]
   use_fully_qualified_names = False
   fallback_homedir = /home/%u
   @end
   - Then restart
   @code bash
   sudo systemctl restart sssd
   @end

## How to list users with a full qualified domain name

   @code bash
   sudo samba-tool user list --full-dn
   @end

## How to create an OU in samba AD DC

   @code bash
   sudo samba-tool ou create "OU=OU_NAME"
   @end

## How to fix deprecation of arcfour-hmac encryption type
   - Edit the file `/etc/krb5/krb5.conf` or `/etc/krb5.conf`
   @code ini
   [libdefaults]
   default_realm = YOUR.REALM.COM
   permitted_enctypes = aes256-cts-hmac-sha1-96 aes128-cts-hmac-sha1-96
   default_tgs_enctypes = aes256-cts-hmac-sha1-96 aes128-cts-hmac-sha1-96
   default_tkt_enctypes = aes256-cts-hmac-sha1-96 aes128-cts-hmac-sha1-96
   allow_weak_crypto = false
   @end
   - Ensure active directory user supports thos encryption types. Go to Active Directory Users and Computers -> User's properties and account tab and check:
      - [x] This account supports Kerberos AES 128 bit encryption
      - [x] This account supports Kerberos AES 256 bit encryption
   
