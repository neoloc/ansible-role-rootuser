Rootuser Role
=========

This role is used to configure the root users password and to manage the root users authorized_keys for ssh.

[![Ansible Galaxy](https://img.shields.io/badge/ansible--galaxy-neoloc.rootuser-blue.svg)](https://galaxy.ansible.com/neoloc/ansible-role-rootuser/)


Requirements
------------

```bash
ansible-galaxy collection install ansible.posix
```

Role Variables
--------------

To create an encrypted password, use `ansible-vault encrypt_string`. See `ansible-vault encrypt_string --help` for details. Example:

` ansible-vault encrypt_string 'somelong_complicated_password_here' --name 'pass'`

Preface the command with a space so that it is not stored in your shells history.


| Variable                | Required | Default | Choices                   | Comments                                 |
|-------------------------|----------|---------|---------------------------|------------------------------------------|
| rootuser.enforce_ssh    | yes      | N/A     | true, false               | enforce /root/.ssh/authorized_keys to only contain keys from rootuser.ssh_keys |
| rootuser.enforce_pass   | yes      | N/A     | true, false               | set the roots password if it changed |
| rootuser.ssh.genkey     | yes      | N/A     | true, false               | whether to generate a SSH key for the user in question |
| rootuser.ssh.keybits    | yes      | N/A     | integer                   | specify number of bits in SSH key to create |
| rootuser.ssh.keytype    | yes      | N/A     | string value              | specify the type of SSH key to generate |
| rootuser.ssh.authkeys   | yes      | N/A     | list of string values     | list of ssh keys to add to /root/.ssh/authorized_keys |
| rootuser.pass           | yes      | N/A     | ansible-vault encrypted string | password to use if setting the root password |

```yaml
rootuser:
  enforce_ssh: true
  enforce_pass: true
  ssh:
    genkey: true
    keybits: 3072
    keytype: rsa
    authkeys:
      - ssh-rsa AAAAB3NzaC1yc2EAAAADAQABAAABAQDtHyA+hGc7cgtH/2v3h9pnZ2BvHY8pHt2Ycoc9G+L+2QgychGc7ofB2oduB5pNisaH0n/evQbl8QI0ff3VGKMI5bj6HbR0zze1nix8jHhO5tgEmn5M+gCiUoTbbEcMPpgrCq7oE1yTuto3ce95t7EXZZDGUv7SLEu/orf3UM1nQMOfFm5RkxM353Mx3AytSOWg6bdFKowOSv66wTqJt7Kpmk5jPQtpBSM5X+ylphJWW3/HqWcJYvdT0LPezlV/a3o6LLzMTujgNdPwsJi7zyS0WAktL/s5j1ugL2hq5AVLWg6fKYH9fVlTcX45UIHYhv57oodv4W3RwRz3nuZQUuTV ben@samaritan
  pass: !vault |
          $ANSIBLE_VAULT;1.1;AES256
          34303130646161666234393831633033643166383737346661316139356133623434306236663739
          3638373939636633346561633137623064326134333235360a396135383165616263363036346135
          32313838323765623332616535363463306566356164653534333161346563666531396263666365
          3334333962303137310a653462306565353131663165656565646130333862356162663466626534
          38616262636131393165636365396530323536316232313963393864653766326632
```

Dependencies
------------

None.

Example Playbook
----------------

Including an example of how to use your role (for instance, with variables passed in as parameters) is always nice for users too:

    - hosts: all
      roles:
         - neoloc.rootuser

License
-------

See license.md

Author Information
------------------

[![Github](https://img.shields.io/badge/Github-neoloc-blue.svg)](https://github.com/neoloc)
