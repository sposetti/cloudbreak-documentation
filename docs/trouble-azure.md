## Troubleshooting Cloudbreak on Azure 

### Credential Creation Errors

#### Role already exists

Example error message: *<span class="cfn-output3">Role already exists in Azure with the name: CloudbreakCustom50</span>*

**Symptom**: You specified that you want to create a new role for Cloudbreak credential, but an existing role with the same name already exists in Azure. 

**Solution**: You should either rename the role during credential creation or select the `Reuse existing custom role` option. 

#### Role does not exist

Example error message: *<span class="cfn-output3">Role does not exist in Azure with the name: CloudbreakCustom60</span>*

**Symptom**: You specified that you want to reuse an existing role for your Cloudbreak credential, but that particular role does not exist in Azure.

**Solution**: You should either rename the new role during the credential creation to match the existing role's name or select the `Let Cloudbreak create a custom role` option. 

#### Role does not have enough privileges 

Example error message: *<span class="cfn-output3">CloudbreakCustom 50 role does not have enough privileges to be used by Cloudbreak!</span>  
<span class="cfn-output3">Please contact the documentaion for more information!</span>*

**Symptom**: You specified that you want to reuse an  existing role for your Cloudbreak credential, but that particular role does not have the necessary privileges for Cloudbreak cluster management.

**Solution**: You should either select an existing role with enough privileges or select the `Let Cloudbreak create a custom role` option.
 
The necessary action set for Cloudbreak to be able to manage the clusters includes:
        `"Microsoft.Compute/*",
        "Microsoft.Network/*",
        "Microsoft.Storage/*",
        "Microsoft.Resources/*"`
 
#### Cloud not validate publickey certificate

Example error message: *<span class="cfn-output3">Could not validate publickey certificate [certificate: 'fdfdsf'], detailed message: Corrupt or unknown public key file format</span>*

**Symptom**: The syntax of your SSH public key is incorrect.

**Solution**: You must correct the syntax of your SSH key. For information about the correct syntax, refer to [this](https://tools.ietf.org/html/rfc4716#section-3.6) page.
