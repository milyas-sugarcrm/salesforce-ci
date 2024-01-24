# Salesforce CI!

Using Github actions, CI is created for PR validations and basic checks. It has two stages:

1.  format-lint-lwc-tests
2.  scratch-org-test

**_format-lint-lwc-tests_**

- Run Prettier
- Run Lint
- Run LWC Test cases

**_scratch-org-test stage_**

- Validates the [PMD rules](https://pmd.github.io/pmd/pmd_rules_apex.html) on the PMD secrets configuration. If there is no PMD rule configured then it will check the default rules defined in pmdrules/defaul.xml. All other rules also defined in pmdrules folder.
- Once PMD rules validates, then it will authenticate the Org using the **DEVHUB*SFDX*** secrets. Create and deploy the scratch org by checking the DailyScratchOrgs limit of license.
- Run SFDX Scanner and upload the results as artifact
- Run Specific Apex Test Classes [Only those created in a PR] and upload the results as artifact
- Upload code coverage to Codecov.io if **CODECOV_TOKEN** is provided

# Installation

**_Pre-requisite_**

1.  Salesforce Instance with Scratch Org creation permission. Scratch orgs available in: **Developer**, **Enterprise**, **Group**, and **Professional** Editions.
2.  [Dev Hub Enabling](https://developer.salesforce.com/docs/atlas.en-us.sfdx_dev.meta/sfdx_dev/sfdx_setup_enable_devhub.htm)
3.  [Connected App](https://developer.salesforce.com/docs/atlas.en-us.sfdx_dev.meta/sfdx_dev/sfdx_dev_auth_connected_app.htm) in Salesforce (Production instance)
4.  Digital Certificates created in setp one using [Create a Private Key and Self-Signed Digital Certificate](https://developer.salesforce.com/docs/atlas.en-us.sfdx_dev.meta/sfdx_dev/sfdx_dev_auth_key_and_cert.htm)
5.  [Prettier Code Formatter](https://developer.salesforce.com/tools/vscode/en/user-guide/prettier)

**_Installation_**

1.  Clone the Repo
2.  Add your Salesforce code in force-app folder
3.  Configure the Repo Secrets in Settings -> Secrets and Variables -> Actions -> Repository secrets

**_Secrets_**
We categorized the secrets into three categories.

-_DevHub Secrets_

1.  DEVHUB_SFDX_CLIENT_ID [ConsumerKey/Client ID of Connect App created in Step 3 of Pre-requisite]
2.  DEVHUB_SFDX_JWT_SERVER_KEY [.key file contents created in Step 3 and 4 of Pre-requisite]
3.  DEVHUB_SFDX_JWT_USERNAME [Production instance username]
4.  DEVHUB_SFDX_JWT_INSTANCE_URL [https://login.salesforce.com]
5.  DEVHUB_SFDX_JWT_ALIAS [Any string like DevHub]

-_PMD Secrets_
Values of these secrets can be either true of false. True means, following rules will validate.

1.  PMD_RULE_BESTPRACTICES
2.  PMD_RULE_CODESTYLE
3.  PMD_RULE_DESIGN
4.  PMD_RULE_DOCUMENTATION
5.  PMD_RULE_ERRORPRONE
6.  PMD_RULE_PERFORMANCE
7.  PMD_RULE_SECURITY

-_CodeCov Secrets_

1. CODECOV_TOKEN [https://codecov.io/ connection with Github and then take the token for the respected repo]

## Other Useful commands

Following commands are added that you can run locally before committing the code:

1.  npm run prettier [To prettify all the files]
2.  npm run lint [To verify the linter]
3.  npm run scanner [To create the SFDX Scanner Report]
4.  npm run prettier:verify [To verify if all files are prettify or not]
5.  npm run test [To run LWC tests]

> If you have any issue or problem, please email to
> muhammad.ilyas@rolustech.com or create an issue.
