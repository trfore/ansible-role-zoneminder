# Ansible Role: ZoneMinder

Install [Zoneminder] on Debian 10-11; and Ubuntu 20.04 & 22.04.

## Role Variables

- ZM Installation Variables:

  | Variable               | Default  | Description                                                                              | Required |
  | ---------------------- | -------- | ---------------------------------------------------------------------------------------- | -------- |
  | `zoneminder_db`        | `mysql`  | String, database backend - `MariaDB` or `MySQL`                                          | No       |
  | `zoneminder_db_user`   | `zmuser` | String, database username for ZM                                                         | No       |
  | `zoneminder_db_pass`   | `zmpass` | String, database password for ZM                                                         | No       |
  | `zoneminder_secure_db` | `false`  | Boolean, secure the database - drop 'test' db, remove anonymous users, set root password | No       |
  | `zoneminder_smtp`      | `false`  | Boolean, install SMTP packages, `msmtp` and `mailutils`, for sending ZM notifications    | No       |

## Dependencies

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

- [Zoneminder]
- [Zoneminder Docs]
- [Zoneminder Repo]
- [Zoneminder Wiki]
- [GitHub: Zoneminder]

[GitHub: Zoneminder]: https://github.com/ZoneMinder/ZoneMinder/
[Zoneminder]: https://zoneminder.com/
[Zoneminder Docs]: https://zoneminder.readthedocs.io/en/latest/index.html
[Zoneminder Repo]: https://zmrepo.zoneminder.com/
[Zoneminder Wiki]: https://wiki.zoneminder.com
