Opencore.Keystores
==================

This role facilitates setting up a PKI infrastructure and signing server and user certificates with that infrastructure.

For a more extensive introduction see this [blog post](http://www.opencore.com/blog/2018/8/keystore-generator/) .

Requirements
------------

This role is not designed to be executed against many hosts and perform changes on these hosts. Instead it should be run against localhost and generate files there based on information from the inventory.
Hence the local (or remote if run against a different one) host has to provide the following software as prerequisites:
- OpenSSL
- Java (for keytool command)

Role Variables
--------------

The role has one mandatory variable which needs to be set for it to run:
KEYSTORE_BASE_DIR: This will be the base path relative to which any files will be created. If this role is used from the [wrapper script ](https://github.com/opencore/keystore_generator) this will automatically be set to the current directory.

To configure the role the following parameters are available:

| Variable               | Description                                                                                                                                                                                           | Default              |
|:-----------------------|:------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|:---------------------|
| CLIENT_CERTIFICATES    | A list of usernames that client certificates will be generated for.                                                                                                                                   | \["user1", "user2"\] |
| CERTIFICATE_VALID_DAYS | The number of days that certificates will be valid for.                                                                                                                                               | 365                  |
| KEY_VALID_DAYS         | The number of days that keys will be valid for.                                                                                                                                                       | 10000                |
| SSL_STORE_PASSWORD     | The password to use for keystore files.                                                                                                                                                               | secret               |
| SSL_KEY_PASSWORD       | The password to use for keys within keystores.                                                                                                                                                        | secret               |
| FORCE_CA               | If set to true any existing files for this inventory will be removed and a completely new set of CA, user and server files will be generated.                                                         | false                |
| FORCE_CERTS            | If set to true the CA files will be kept but all user and server keys and certificats will be regenerated. Useful if your user certificates expired and you want to regenerate them from the same CA. | false                |
| DOMAIN                 | Used for certificate properties.                                                                                                                                                                      | OPENCORE.COM         |
| O                      | Used for certificate properties.                                                                                                                                                                      | OpenCore             |
| C                      | Used for certificate properties.                                                                                                                                                                      | DE                   |
| ST                     | Used for certificate properties.                                                                                                                                                                      | SH                   |
| L                      | Used for certificate properties.                                                                                                                                                                      | Wedel                |
| OU                     | Used for certificate properties.                                                                                                                                                                      | Internal             |
| KEYSTORE_DIR           | Path to directory which will contain keystores. Should usually not be necessary to change this.                                                                                                       |                      |
| CA_DIR                 | Path to directory which will contain ca files. Should usually not be necessary to change this.                                                                                                        |                      |
| CERT_DIR               | Path to directory which will contain intermediate certificate and csr files. Should usually not be necessary to change this.                                                                          |                      |


Dependencies
------------

The role has no direct dependecies on other roles.


Example Playbook
----------------

Including an example of how to use your role (for instance, with variables passed in as parameters) is always nice for users too:

```yaml
- hosts: localhost
  roles:
    - opencore.keystores
```
License
-------

BSD

