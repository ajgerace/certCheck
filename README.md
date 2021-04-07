# CertCheck

Ansible playbook to check the certificate associated with client-ssl profiles for expiration with-in a user defined number of days.


This ansible playbook (automateCerts.yml) has been designed to utilize 3 roles (checkExpire, createCsrCert and installNewKeysCerts ).
Any variables that are specific to a given role are placed in the roles _vars/main.yml_ file.

Authentication users accounts are defined in _group_vars/all/users.yml_ file, with username and password variables being pulled from two environment variables.

The _checkExpire/vars/crts2Check.yml_ file contains a dictionary of dictionarires  of which clientssl profiles certificates are to be checked.
Sample of the crt2Check.yml file format.
```
---
    certs2Check:
      astro.thejetsons.org_clientssl:
        host: 192.168.0.49
        partition: Common
      elroy.thejetsons.org_clientssl:
        host: 192.168.0.45
        partition: Common
      judy.thejetsons.org_clientssl:
        host: 192.168.0.45
        partition: Common
```

The number of days in the future to check for certificate expiration is handled with the _crtExpireCheckDate_ variable.

_certNames2Renew_ is a dictionary of dictionaries that keyed by the clientssl profile name.

Example:
```
astro.thejetsons.org_clientssl:
  commonName: astro.thejetsons.org
  expiration: 2021-04-02 15:58:01
  host: 192.168.0.49
  partition: Common  
```

Currently the createCsrCert creates self assigned certificates with a user-defined number of days controlled by the _certDays_ variable located in the _createCsrCert/vars/main.yml_ file.   

The new SSL keys and certs will have a timestamp appended to their names. The timestamp variable is defined in _automateCerts.yml_ file.

 Example: _elroy.thejetsons.org-2021-04-07.key_

