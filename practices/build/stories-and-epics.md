# Stories & Epics

## Consider security needs on every story or epic

The Security Champion should be actively involved in defining security needs within user stories. Security Champions should help the team define the security acceptance criteria and engage with Security Engineers for more specialist support when required. For example, implementing features using cryptography may require assistance or review from a Security Engineer. Consideration should be given to defining sufficient test cases to meet the security needs, e.g. ensuring an unauthenticated user is not able to access protected functionality. Consideration should also be given to whether any known risks for the product are impacted by this change, which should be updated as appropriate.

The Security Champion should be responsible for ensuring that security is considered for every story. This is an opportunity for Security Champions to develop their knowledge and experience with assistance from Security Engineers, and will gradually make the delivery team more independent. It will also help the Security Engineers to focus their time on the most critical or complex cases where specialist support is needed.

## Iterative and incremental threat modelling

We should do threat modelling whenever there's a significant change to the product. When creating epics and stories, we must consider whether the architectural threat model needs to be updated or whether there needs to be a specific threat model created for this change. The objective is to identify whether any security controls need to change or be added to maintain the security of the product.

Creating threat models in response to each change ensures the activity is focused. Consider timeboxing threat modelling activity to ensure maximum effectiveness - teams are more likely to continue with this practice if it is not too time consuming.

Also consider whether any known risks for the product are impacted by this change, and update the risks as appropriate.

## Security Engineers should review security-critical changes

Some code has a higher impact on the security of the product, such as code handling authentication. In addition, some changes are more complex and require specialist experience to ensure it is secure, such as cryptography. Defining sufficient test cases can be difficult, and often benefits from having someone with security experience available to help.

Sections of security-critical code should be reviewed by experienced Security Engineers. It is possible to integrate this into source control to prevent security-critical code from being merged until it has been reviewed, for example by tagging associated stories. Alternatively, this can also be achieved by having a good close working relationship with Security Engineers so they are aware and available to help when needed.

