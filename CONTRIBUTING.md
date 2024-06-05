# Contributing

## Contribute

- [Fork the repository](https://github.com/trfore/ansible-role-zoneminder/fork) on github and clone it.
- Create a new branch and add your code.
- Write test that cover the changes and expected outcome.
- Test your changes locally using `tox`.
- Push the changes to your fork and submit a pull-request on github.

```sh
git clone https://github.com/USERNAME/ansible-role-zoneminder && cd ansible-role-zoneminder
git checkout -b MY_BRANCH
# add code and test
tox run-parallel
git push -u origin MY_BRANCH
gh pr create --title 'feature: add ...'
```

### Setup a Dev Environment

```sh
cd ansible-role-zoneminder
python3 -m venv .venv && source .venv/bin/activate
python3 -m pip install -r requirements/dev-requirements.txt
pre-commit install
```

### Tox: Test Suite

- A local installation of [Docker](https://docs.docker.com/engine/installation/) is required to run the `molecule` test
  scenarios.
- All `tox` environments are created within the project directory under `.tox`.
- The collection is tested using the latest version of `ansible-core` on CentOS, Debian and Ubuntu image.
- Extensive code modifications that change how a playbook is written need to be accompanied by test, e.g. molecule
  scenario, that covers the changes. This will help avoid end-user frustration with faulty code examples in the
  documentation.

  ```sh
  cd ansible-role-zoneminder
  # list environments and test
  tox list
  # lint all files
  tox -e lint run
  # run a specific test environment
  tox -e py-ansible2.16-ubuntu22-default run
  # run a group of tests, e.g. the default molecule scenario
  tox -f default run
  # run all test in parallel
  tox run-parallel
  ```

- For iterative development and testing, the tox molecule environments are written to accept `molecule` arguments. This
  allows for codebase changes to be tested as you write across multiple distros and versions of `ansible-core`.

  ```sh
  # molecule converge
  tox -e py-ansible2.16-ubuntu22-default run -- converge -s default
  # molecule test w/o destroying the container
  tox -e py-ansible2.16-ubuntu22-default run -- test -s default --destroy=never

  # exec into the container via tox
  tox -e py-ansible2.16-ubuntu22-default run -- login -s default
  # exec into the container
  docker exec -it py-ansible2.16-ubuntu22-default bash

  # parallel testing
  tox -f default run-parallel -- test -s default --destroy=never
  # remove all containers
  tox -f default run-parallel -- destroy -s default
  ```

### Documentation

- New features or extensive code changes need to be accompanied by documentation in a `argument_specs.yml` and README.
  This information can be redundant, yet it is often helpful to start with the argument_specs then copy it to a README.

### Pull Request

- All pull request are run through a more extensive test suite that will validate the collection on multiple OSs and
  releases, yet local `pre-commit` and `tox` test should provide a good proxy for the github tests.

## Additional References

- [Ansible community guide](https://docs.ansible.com/ansible/devel/community/index.html)
- [Github Docs: Forking a repository](https://docs.github.com/en/pull-requests/collaborating-with-pull-requests/working-with-forks/fork-a-repo#forking-a-repository)
- [Ansible Docs: `ansible-core` support matrix](https://docs.ansible.com/ansible/latest/reference_appendices/release_and_maintenance.html#ansible-core-support-matrix)
