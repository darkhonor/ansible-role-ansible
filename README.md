# Ansible Role: Ansible

Installs the Ansible Core application and (if required) the modules and
plugins required to operate the application in an airgap environment.

## Requirements

None

## Role Variables

You can modify any of the following variables as you wish in the role's `defaults/main.yml`:

* `airgap`: Boolean if the target is in an airgap'd environment (Default: `false`)
* `trust_repository_certs`: Boolean if the source repository's certificate is trusted by the target (Default: `true`)
* `collection_archive_url`: Full URL to an archive of the Ansible Collections (airgap only)
* `python_lib_archive_url`: Full URL to an archive of the Python Libraries required by Ansible (airgap only)
* `collection_archive_path`: Path on the target to create and store the Ansible Collections (airgap only; Default: `/opt/ansible`)
* `python_archive_path`: Path on the target to create and store the Python Library archive before installation (airgap only; Default: `/opt/python-libs`)

The following role variables are *safe* defaults and should not need to be modified:

* `collection_archive_owner`: File owner for the collection archive (airgap only; Default: `root`)
* `collection_archive_group`: Group owner for the collection files (airgap only; Default: `root`)
* `collection_archive_mode`: Directory Mode for the collection files (airgap only; Default: `0755`)
* `collection_archive_setype`: SELinux Type for collection files (airgap only; Default: `usr_t`)
* `collection_archive_keep_newer`: Boolean if you want to preserve files locally that are newer than the files in the archive (airgap only; Default: `false`)
* `ansible_collection_list`: Curated list of Ansible Collections to install with the role (airgap only)
* `python_library_list`: Curated list of Python Libraries to install with the role (airgap only)

## Dependencies

None

## Example Playbook

Here is an example playbook using this role:

```yaml
- name: Configure workstations
  become: true
  become_method: sudo
  gather_facts: true
  hosts: all
  roles:
    - role: ansible
      airgap: true
      trust_repository_certs: false
      collection_archive_url: "{{ repo_server }}/{{ ansible_collection_archive }}"
      collection_archive_path: /opt/ansible
      python_archive_path: /opt/python-libs
      ansible_collection_list: '{{ ansible_collection_archive_list }}'
      python_library_list: '{{ python_libs_list }}'
```

## License

MIT

## Author Information

Alex Ackerman, GitHub @darkhonor
