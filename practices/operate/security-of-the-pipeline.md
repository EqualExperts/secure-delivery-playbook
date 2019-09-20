# Security of the Pipeline

The pipeline produces the product artefacts that are deployed into production. In order to trust that these artefacts have been correctly produced without vulnerabilities or malicious code being introduced, the security of the pipeline needs to be as good as the security of the product itself.

## Harden the pipeline as a production system

In addition to [infrastructure hardening](environment-provisioning.md#automate-infrastructure-hardening), build pipelines have unique characteristics that must be addressed in order to preserve their security. Failing to do this can lead to a compromise of the build system.

For example, builds should not be allowed to run on Jenkins master nodes as this has [serious security implications](https://wiki.jenkins.io/display/JENKINS/Security+implication+of+building+on+master) and been used to compromise Jenkins administrator accounts in the past. Relevant security controls should be enabled and default user accounts should be changed on all pipeline systems. All build plugins should be carefully vetted to avoid introducing vulnerabilities in a [similar way to all product dependencies](../build/security-in-the-pipeline.md#establish-provenance-of-third-party-components). These should be kept up to date with the latest security patches.

## Monitor the pipeline as a production system

Pipelines are production systems in their own right, and therefore warrant the same attention to monitoring and alerting as any live system would. Failing to do this prevents you from identifying anomalous behaviour \(such as failed login attempts, etc.\) and hinders your ability to investigate in the event of an incident.

CI/CD pipelines should have a centralised logging and monitoring infrastructure in place that all components \(e.g. source control, build servers, artefact repositories, etc.\) feed into, so that suspicious behaviour can be detected and alerted on.

## Manage secrets securely

Pipelines require access to various external systems, such as source repositories, artefact repositories and target environments for deployment. This provides an attacker with the ability to control infrastructure or deployments, access secrets, or anything else involved in building, packaging and deploying code.

Wherever possible, avoid the need to manage secrets directly and use native platform features that handle this on your behalf. For example, cloud providers offer identity and access management features, such as AWS IAM and GCP Cloud Identity and Access Management, that enable workloads to be authorised while automatically handling key/credential rotation, auditing, etc.

Within the pipeline, all secrets should be stored and managed securely, ideally using a [secrets management system](environment-provisioning.md#centralised-and-automated-secret-management). Where it's not possible to use a central secrets management system, it's important to understand what controls are provided by the pipeline tools and their limitations.

The principle of least privilege should be applied for secrets \(e.g. read only access to source control\). This includes using unique credentials for the build pipeline, so that it can be traced back if suspicious activity is detected.

Be aware that secrets may be accidentally or intentionally exposed via build logs, and mechanisms should be put in place to detect this or prevent it from happening if possible.

