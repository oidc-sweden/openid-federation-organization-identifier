![Logo](https://www.oidc.se/img/oidc-logo.png)

# OpenID Federation Organization Identifier Metadata Parameter  1.0

An Entity within a federation is, in almost all cases, owned by an organization. In many cases, an actor within the federation needs to know which organization that is behind a given Entity. Reasons for this may be invoicing, bilateral agreements or accountability. Therefore, an Entity needs to have a mechanism to uniquely represent the organization to which it belongs.

This specification defines the `organization_identifier` metadata parameter that allows Entities to declare an unique organization identifier.

## Builds

<!--
The latest released draft of the specification is available at [https://www.oidc.se/specifications/openid-federation-organization-identifier-1_0.html](https://www.oidc.se/specifications/openid-federation-organization-identifier-1_0.html).
-->

Previews for each branch are automatically built and published. You can view the preview of the main branch at [https://www.oidc.se/openid-federation-organization-identifier/main.html](https://www.oidc.se/openid-federation-organization-identifier/main.html).
Other branches are built and deployed as well, using the branch name as the HTML filename, as shown below:

> `https://www.oidc.se/openid-federation-organization-identifier/$BRANCH-NAME.html`

## Build the HTML ##

```docker run -v `pwd`:/data danielfett/markdown2rfc openid-federation-organization-identifier-1_0.md```

## Contact

For further information and to get involved, please contact the authors.
