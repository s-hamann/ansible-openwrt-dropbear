OpenWRT Dropbear
================

This role configures [Dropbear](https://matt.ucc.asn.au/dropbear/dropbear.html) on [OpenWRT](https://www.openwrt.org/) targets.
It can also set up SSH public key authentication for the `root` user.

Requirements
------------

This role has no special requirements on the controller.

It does, however, require a working [Python](https://www.python.org/) installation on the target system or [gekmihesg's Ansible library for OpenWRT](https://github.com/gekmihesg/ansible-openwrt) on the Ansible controller.

Role Variables
--------------

* `dropbear_config`  
  A dictionary of uci configuration options for Dropbear.
  Refer to the [documentation](https://openwrt.org/docs/guide-user/base-system/dropbear) for valid keys and their meaning.
  This role's default configuration deviates from OpenWRT's in two points:
  * `Interface` is set to `lan`
  * `PasswordAuth` and `RootPasswordAuth` are disabled if `dropbear_user_public_key` is set.
* `dropbear_user_public_key`  
  A list of SSH public key that are added to the global `authorized_keys` file of the `root` user.
  SSH key public key can be given as the keys themselves or as paths to the public key files on the Ansible controller.
  Optional.
* `dropbear_enable_sftp`  
  If set to `true`, this role installs [OpenSSH](https://www.openssh.com/)'s SFTP server component so that the SFTP subsystem an be used with the target system.
  Defaults to `false`.

Dependencies
------------

This role does not depend on any specific roles.

Example Configuration
---------------------

The following is a short example for some of the configuration options this role provides:

```yaml
dropbear_config:
  Port: 2222
  Interface: "{{ omit }}"
dropbear_user_public_key:
  - ~/.ssh/id_ed25519.pub
```

License
-------

MIT
