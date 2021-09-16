# vault_pam_helper
Python PAM helper module to authenticate against HashiCorp Vault

# Usage

Make sure you have installed the **python-pam-module**. This allows you to run a Python application as a PAM module

Place the **vault-pam-helper.py** somewhere on your system, for example in **/usr/local/bin**

Next, add a section in your PAM stack, for example in **/etc/pam.d/sshd** to allow users to authenticate using their Vault user_pass password:

```
auth    [success=2 default=ignore]  pam_python.so /usr/local/bin/vault-pam-helper.py vault_addr=<your VAULT URL> nosslverify debug prompt="Vault_Or_Local_Password"
auth    [success=1 default=ignore]  pam_unix.so nullok_secure
auth    requisite                   pam_deny.so
auth    required                    pam_permit.so
```
# Config options

| option | meaning | default |
| - | - | - |
| debug | Turn on debugging | no debugging |
| prompt | Use this text as the promt for the user | Vault Password |
| vault_addr | Use this url to connect to Vault | http://localhost:8200 |
| nosslverify | Disable SSL verify | default off |
| cacerts | the CA cert file to use to verify the VAULT SSL Certificate | /etc/ssl/certs/myCA.pem |

*Acknowledgement:*

Part of the code taken from [PrivacyIDEA](https://github.com/privacyidea/pam_python/blob/master/privacyidea_pam.py)


