# Ansible collection: kangaroot.foreman_content_elrepo

Collection for configuring ELRepo.org Community Enterprise Linux repositories in a Foreman/Katello installation.

The ELRepo.org Community Enterprise Linux repositories that can be configured from this collection are:

- ELRepo.org Community Enterprise Linux (elrepo, kernel and extras):
  - EL7 (x86_64)
  - EL8 (x86_64)[^1]
  - EL9 (x86_64)[^1]

[^1]: Enabled by default when enabling ELRepo.org Community Enterprise Linux repositories.

## Requirements and Dependencies

Ansible Core 2.13.0 or higher is required for the roles in the collection.

The roles in this collection must be imported by the `kangaroot.foreman` collection. It is possible to directly use the roles in this collection but not recommended.

The `kangaroot.foreman` collection requires the `theforeman.foreman` and `theforeman.operations` collections. To install the required collections, execute:

```shell
ansible-galaxy collection install -r requirements.yml
```

in the collection directory.

## Collection Variables

The `group_vars` directory contains example vars files for the important variables used in the collection roles.

## Usage

The variable `foreman_content_roles` from the `foreman` role in the `kangaroot.foreman` collection contains a list content roles to import.

Add this collection content role to the `foreman_content_roles` list of content roles to import in your playbook project variables.

For example, add the `foreman_content_roles` variable in your `group_vars/foreman.yml` file of your playbook project:

```yaml
# Foreman content roles to include
foreman_content_roles:
  # Package only content
  - kangaroot.foreman_content_elrepo.foreman_content_elrepo
  - ...

  # OS content
  - kangaroot.foreman_content_rocky.foreman_content_rocky
  - ...

  # Builtin content
  - kangaroot.foreman_content_builtin.foreman_content_builtin
```

Also ensure that the ELRepo.org Community Enterprise Linux repositories are enabled and at least one of the ELRepo.org Community Enterprise Linux OS related repositories is enabled as well by setting the appropriate enable variables:

```yaml
foreman_enable_elrepo: true
foreman_enable_elrepo_el8: true
foreman_enable_elrepo_el9: false
```

In your playbook, add a task to execute the `kangaroot.foreman.foreman` role:

```yaml
- name: Run kangaroot.foreman roles
  hosts: foreman
  roles:
    - kangaroot.foreman.foreman
```

