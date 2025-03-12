# Ansible Role - trfore.zoneminder

[![CI](https://github.com/trfore/ansible-role-zoneminder/actions/workflows/ci.yml/badge.svg?branch=main)](https://github.com/trfore/ansible-role-zoneminder/actions/workflows/ci.yml)
[![CD](https://github.com/trfore/ansible-role-zoneminder/actions/workflows/cd.yml/badge.svg?branch=main)](https://github.com/trfore/ansible-role-zoneminder/actions/workflows/cd.yml)

This role will install the following on the target node:

- [Zoneminder] Open-source video surveillance software system.
- [MySQL] or [MariaDB] database backend for Zoneminder (ZM).
- [PyMySQL] for configuring and securing MySQL / MariaDB.

**New to Ansible?** See the [wiki (link)](https://github.com/trfore/ansible-role-zoneminder/wiki/New-User-Guide) for detailed
instructions on setting up Ansible and running this role.

## Install the Role

You can install this role with the Ansible Galaxy CLI:

```bash
ansible-galaxy role install trfore.zoneminder
```

## Tested Platforms

- `ansible-core` 2.16, 2.17 & 2.18
- Debian 11 & 12
- Ubuntu 20.04 & 22.04

## Role Variables

- The Zoneminder package automatically creates a default database user, `zmuser`, and password, `zmpass`, with
  permissions to the `zm` database. Setting `zoneminder_db_user` and `zoneminder_db_pass` will remove the default user
  and configure Zoneminder to use the new username and password.
- **Warning**: The database username and password are limited to 32 characters - alphanumeric, underscore (`_`), and
  dollar-sign (`$`) characters are permitted. However, the first character cannot be `$`. This role **does not validate**
  these inputs, incorrect values will break the install.
- `MySQL` is not available on Debian, `MariaDB` is automatically installed.

  | Variable               | Default   | Description                                                                           | Required |
  | ---------------------- | --------- | ------------------------------------------------------------------------------------- | -------- |
  | `zoneminder_db`        | `mariadb` | String, database backend - `MariaDB` or `MySQL`                                       | No       |
  | `zoneminder_db_user`   | `zmuser`  | String, database username for ZM.                                                     | No       |
  | `zoneminder_db_pass`   | `zmpass`  | String, database password for ZM.                                                     | No       |
  | `zoneminder_secure_db` | `true`    | Boolean, secure the database - drop 'test' db and remove anonymous users              | No       |
  | `zoneminder_smtp`      | `false`   | Boolean, install SMTP packages, `msmtp` and `mailutils`, for sending ZM notifications | No       |

## Dependencies

- `community.general`
- `community.mysql`

## Example Playbook

```yaml
- hosts: servers
  become: true
  pre-task:
    - name: Set Server Timezone
      community.general.timezone:
      name: America/New_York

  roles:
    - name: Install ZM
      role: trfore.zoneminder
```

## License

See [LICENSE](LICENSE) File

## Author Information

Taylor Fore (<https://github.com/trfore>)

## References

- [MariaDB]
- [MariaDB Docs]
- [MySQL]
- [MySQL Docs]
- [PyMySQL]

Zoneminder:

- [Zoneminder]
- [Zoneminder Docs]
- [Zoneminder GitHub Repo]
- [Zoneminder Package Repo]
- [Zoneminder Wiki]
- [GitHub: Zoneminder]

[GitHub: Zoneminder]: https://github.com/ZoneMinder/ZoneMinder/
[MariaDB]: https://mariadb.com/
[MariaDB Docs]: https://mariadb.com/kb/en/documentation/
[MySQL]: https://www.mysql.com/
[MySQL Docs]: https://dev.mysql.com/doc/
[PyMySQL]: https://pymysql.readthedocs.io/en/latest/
[Zoneminder]: https://zoneminder.com/
[Zoneminder Docs]: https://zoneminder.readthedocs.io/en/latest/index.html
[Zoneminder GitHub Repo]: https://github.com/ZoneMinder/zoneminder
[Zoneminder Package Repo]: https://zmrepo.zoneminder.com/
[Zoneminder Wiki]: https://wiki.zoneminder.com
