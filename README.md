# Re-Creating the AAP Platform Auditor Account

The current configuration for scraping AAP metrics has all manifests deployed via ArgoCD.

However, if the AAP cluster is reprovisioned, you will need to re-create the Platform Auditor user and its corresponding token for authentication. Then you will need to update Bitwarden and AWS Secrets Manager respectively. The steps below outline how to do this. 

### Create the Platform Auditor User & Token

1. Log into the AAP cluster (dev/prod). Credentials can be found in Bitwarden.
2. Access Management > Users > Create user
3. Fill in fields, `User type` must be `Ansible Automation Platform Auditor`
4. Click `Create user`
5. Log out and log in as the newly created Platform Auditor user
6. Access Management > Users > `aap-metrics`
7. API Tokens > Create API token
8. Fill in `Description field
9. `Scope`: `Read`
10. Save the generated token

### Update Bitwarden Credentials & Secret in AWS Secrets Manager

1. Update `[Dev/Prod] AAP Platform Auditor Account` in Bitwarden with new log in credentials and token
2. Access `tt-tools-dev` > `TT-ORG-ROSA` or `tt-tools-prod` > `TT-ORG-ROSA` AWS depending on what you need
3. `AWS Secrets Manager` > `dev/aap/aap-metrics` or `prod/aap/aap-metrics`
4. Update the `Secret value` with the newly created token from step `10` in the previous section