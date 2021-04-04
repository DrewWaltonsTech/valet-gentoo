[Main page](index)

<h1><img src="https://www.gentoo.org/assets/img/logo/gentoo-signet.svg" height="40">
Valet Gentoo</h1>

# Requirements
- [Gentoo Linux](#gentoo)
- [Regarding sudo and root user](#sudo)

-----
## <a name="gentoo">Gentoo Linux</a>

Requirement | Description
------------- | -------------
OS packages | `emerge -av dev-libs/nss app-misc/jq x11-misc/xsel net-misc/networkmanager net-dns/dnsmasq sys-fs/inotify-tools`
USE flags | `nss` should be emerged with at least `USE="utils"`. The `utils` flag is required to install certutil.
Nginx packages | Nginx should be installed prior to using Valet Gentoo, but Valet *should* install it for you if not installed. Install with `www-servers/nginx`.
Nginx USE flags | The default nginx USE flags should be fine.
PHP version | PHP ***must*** be installed prior to installing Valet Gentoo. Install with `emerge -av dev-lang/php` ( need **>= 7.3** ; specify version with `emerge -av php:8.0`)
PHP extensions | In Gentoo, USE flags can be set to configure PHP modules. Recommended USE flags are: `acl bcmath berkdb bzip2 cli ctype curl fileinfo filter fpm gd gdbm hash iconv inifile intl ipv6 json ldap mysql mysqli nls opcache pcntl pdo phar posix readline session simplexml spell ssl systemd tokenizer unicode xml xmlreader xmlrpc xmlwriter xslt zip zlib`
AppArmor | In order to use Valet Gentoo when [AppArmor is enabled](https://wiki.gentoo.org/wiki/AppArmor), you will need to modify your system as [mentioned below](#apparmor).
Composer | Install [composer](https://wiki.archlinux.org/index.php/PHP#Composer), php package manager. You may also install composer with `emerge -av dev-php/composer

-----
##<a name="apparmor">Regarding AppArmor</a>

If you wish to use Valet Gentoo with AppArmor, you will need to add the following to `/etc/apparmor.d/local/usr.sbin.dnsmasq`:
```
/opt/valet-linux/dns-servers r,
/proc/sys/kernel/osrelease r,
/proc/1/environ r,
/proc/cmdline r,
```

-----
## <a name="sudo">Regarding `sudo` and `root` user</a>

Valet Gentoo makes automatic use of **`sudo`** to perform some of its tasks. This implies that for Valet to perform correctly your user needs to be configured as a **sudo** user.

Please **do not, under any circumstance, install Valet Gentoo with `root` or the `sudo` command**. Kittens could die.