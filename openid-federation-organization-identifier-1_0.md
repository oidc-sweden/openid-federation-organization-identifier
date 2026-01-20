%%%
title = "OpenID Federation Organization Identifier Metadata Parameter 1.0 - draft 00"
abbrev = "openid-federation-organization-identifier"
ipr = "none"
workgroup = "OpenID Connect A/B"
keyword = ["security", "openid", "ssi"]

[seriesInfo]
name = "Internet-Draft"
value = "openid-federation-organization-identifier"
status = "standard"

[[author]]
initials="M.B."
surname="Jones"
fullname="Michael B. Jones"
organization="Self-Issued Consulting"
    [author.address]
    email = "michael_b_jones@hotmail.com"

[[author]]
initials="M."
surname="Lindström"
fullname="Martin Lindström"
organization="IDsec Solutions"
    [author.address]
    email = "martin@idsec.se"

[[author]]
initials="S."
surname="Santesson"
fullname="Stefan Santesson"
organization="IDsec Solutions"
    [author.address]
    email = "stefan@idsec.se"

%%%

.# Abstract

An Entity within a federation is, in almost all cases, owned by an organization. In many cases, an actor within the federation needs to know which organization that is behind a given Entity. Reasons for this may be invoicing, bilateral agreements or accountability. Therefore, an Entity needs to have a mechanism to uniquely represent the organization to which it belongs.

This specification defines the `organization_identifier` metadata parameter that allows Entities to declare an unique organization identifier.


{mainmatter}

# Introduction

OpenID Federation [@!OpenID.Federation] provides a framework for establishing trust between Entities through cryptographically verifiable metadata and Trust Chains. While this framework enables secure discovery and validation of technical and operational properties of Entities, it does not provide a standard mechanism for identifying the organization that owns or operates a given Entity.

In practice, most Entities within a federation are operated by organizations rather than individuals. Federation participants and operators may therefore need to determine which organization stands behind a particular Entity. This information can be required for purposes such as invoicing, establishing bilateral or contractual agreements, policy enforcement, or accountability and incident handling.

This specification introduces the `organization_identifier` metadata parameter, which allows an Entity to declare a unique identifier for the organization to which it belongs. The identifier is intended to be stable, unambiguous within the federation, and suitable for use in administrative and policy-driven processes. The precise format and semantics of the identifier are federation specific and are expected to be defined by federations that choose to support this parameter.


## Requirements Notation and Conventions

The key words "MUST", "MUST NOT", "REQUIRED", "SHALL", "SHALL NOT", "SHOULD",
"SHOULD NOT", "RECOMMENDED", "NOT RECOMMENDED", "MAY", and "OPTIONAL" in
this document are to be interpreted as described in BCP 14 [@!RFC2119]
[@!RFC8174] when, and only when, they appear in all capitals, as shown here.

## Terminology

This specification uses the terms "OpenID Provider (OP)" and "Relying Party (RP)" as defined by OpenID Connect Core 1.0 [@!OpenID.Core], the terms "Authorization Server (AS)", "Client", and "Protected Resource" defined by OAuth 2.0 [@!RFC6749], and the terms "Entity", "Subordinate Statement", "Intermediate Entity", "Subordinate Entity", and "Superior Entity" defined in OpenID Federation 1.0 [@!OpenID.Federation].

# The organization\_identifier Metadata Parameter {#the_organization_identifier_metadata_parameter}

This specification extends [@!OpenID.Federation] with the following metadata parameter:

`organization_identifier`
: <br>OPTIONAL. A string that uniquely identifies the organization owning this Entity. The format of this identifier is federation specific and SHOULD be defined by federations supporting the parameter. 

```json=
"metadata" : {
  "openid_relying_party" : {
    "organization_name#en" : "Example Company",
    "organization_name#sv" : "Exampelföretaget",
    "organization_identifier" : "0195:5590026352",
    ...
  }
},
```

**Example**: An excerpt of an OpenID Relying Party's metadata where the Entity is owned by the "Example Company". This company is in this example uniquely identified using the [ISO/IEC 6523](https://www.iso.org/standard/82246.html) identifier for the organization.

# Security Considerations

## Trusting the Organization Identifier

Allowing an Entity to declare the `organization_identifier` value in its own metadata introduces potential risks if this value is not subject to appropriate controls. In particular, an Entity could falsely claim association with an organization to which it does not belong. If other federation participants rely on this value without additional validation, this could lead to incorrect trust decisions, misdirected contractual relationships, or incorrect attribution of responsibility.

To mitigate this risk, federations MAY apply policies that ensure that the `organization_identifier` value is constrained and validated by the Superior Entity before it is relied upon. One effective mitigation is for the Superior Entity to define a fixed `organization_identifier` value in its metadata policy for a Subordinate Entity. This prevents the Subordinate Entity from arbitrarily setting or changing this value.

By enforcing the value for `organization_identifier` through metadata policy, the Superior Entity effectively vouches for the association between the Entity and the identified organization.

```json=
"metadata_policy" : {
  "openid_relying_party": {
    "organization_identifier": {
      "value": "0195:5590026352"
    }
  }
}
```

**Example**: An example of a metadata policy in a Subordinate Statement where the `organization_identifier` is set to a fixed, and validated, value. 

# IANA Considerations

## OAuth Dynamic Client Registration Metadata Registration

This specification registers the following client metadata entry in the IANA "OAuth Dynamic Client Registration Metadata" registry [@!IANA.OAuth.Parameters] established by [@!RFC7591].

* Client Metadata Name: `organization_identifier`
* Client Metadata Description: A string that uniquely identifies the organization that owns a Client/RP
* Change Controller: OpenID Foundation Artifact Binding Working Group - openid-specs-ab@lists.openid.net
* Specification Document(s): (#the_organization_identifier_metadata_parameter) of this specification

## OAuth Authorization Server Metadata Registration

This specification registers the following metadata entries in the IANA "OAuth Authorization Server Metadata" registry [@!IANA.OAuth.Parameters] established by [@!RFC8414].

* Metadata Name: `organization_identifier`
* Metadata Description: A string that uniquely identifies the organization that owns an AS/OP
* Change Controller: OpenID Foundation Artifact Binding Working Group - openid-specs-ab@lists.openid.net
* Specification Document(s): (#the_organization_identifier_metadata_parameter) of this specification

## OAuth Protected Resource Metadata Registration

This specification registers the following protected resource metadata entries in the IANA "OAuth Protected Resource Metadata" registry [@!IANA.OAuth.Parameters] established by [@!RFC9728].

* Metadata Name: `organization_identifier`
* Metadata Description: A string that uniquely identifies the organization that owns a Protected Resource
* Change Controller: OpenID Foundation Artifact Binding Working Group - openid-specs-ab@lists.openid.net
* Specification Document(s): (#the_organization_identifier_metadata_parameter) of this specification


# Acknowledgments

We would like to thank the following individuals for their comments, ideas, and contributions to this implementation profile and to the initial set of implementations.

- X Y, Z

{backmatter}

<reference anchor="OpenID.Core" target="http://openid.net/specs/openid-connect-core-1_0.html">
  <front>
    <title>OpenID Connect Core 1.0 incorporating errata set 2</title>
    <author initials="N." surname="Sakimura" fullname="Nat Sakimura">
      <organization>NRI</organization>
    </author>
    <author initials="J." surname="Bradley" fullname="John Bradley">
      <organization>Ping Identity</organization>
    </author>
    <author initials="M." surname="Jones" fullname="Michael B. Jones">
      <organization>Microsoft</organization>
    </author>
    <author initials="B." surname="de Medeiros" fullname="Breno de Medeiros">
      <organization>Google</organization>
    </author>
    <author initials="C." surname="Mortimore" fullname="Chuck Mortimore">
      <organization>Salesforce</organization>
    </author>
   <date day="15" month="December" year="2023"/>
  </front>
</reference>

<reference anchor="OpenID.Federation" target="https://openid.net/specs/openid-federation-1_0.html">
  <front>
    <title>OpenID Federation 1.0</title>
    <author fullname="R. Hedberg, Ed.">
      <organization>independent</organization>
    </author>
    <author fullname="Michael B. Jones">
      <organization>Self-Issued Consulting</organization>
    </author>
    <author fullname="A. Solberg">
      <organization>Sikt</organization>
    </author>
    <author fullname="John Bradley">
      <organization>Yubico</organization>
    </author>
    <author fullname="Giuseppe De Marco">
      <organization>independent</organization>
    </author>
    <author fullname="Vladimir Dzhuvinov">
      <organization>Connect2id</organization>
    </author>
    <date day="4" month="December" year="2025"/>
  </front>
</reference>

<reference anchor="IANA.OAuth.Parameters" target="https://www.iana.org/assignments/oauth-parameters">
  <front>
    <title>IANA, "OAuth Parameters"</title>
    <author>
      <organization>IANA</organization>
    </author>
    <date/>    
  </front>
</reference>

# Notices

Copyright (c) 2026 The OpenID Foundation.

The OpenID Foundation (OIDF) grants to any Contributor, developer, implementer, or other interested party a non-exclusive, royalty free, worldwide copyright license to reproduce, prepare derivative works from, distribute, perform and display, this Implementers Draft or Final Specification solely for the purposes of (i) developing specifications, and (ii) implementing Implementers Drafts and Final Specifications based on such documents, provided that attribution be made to the OIDF as the source of the material, but that such attribution does not indicate an endorsement by the OIDF.

The technology described in this specification was made available from contributions from various sources, including members of the OpenID Foundation and others. Although the OpenID Foundation has taken steps to help ensure that the technology is available for distribution, it takes no position regarding the validity or scope of any intellectual property or other rights that might be claimed to pertain to the implementation or use of the technology described in this specification or the extent to which any license under such rights might or might not be available; neither does it represent that it has made any independent effort to identify any such rights. The OpenID Foundation and the contributors to this specification make no (and hereby expressly disclaim any) warranties (express, implied, or otherwise), including implied warranties of merchantability, non-infringement, fitness for a particular purpose, or title, related to this specification, and the entire risk as to implementing this specification is assumed by the implementer. The OpenID Intellectual Property Rights policy requires contributors to offer a patent promise not to assert certain patent claims against other contributors and against implementers. The OpenID Foundation invites any interested party to bring to its attention any copyrights, patents, patent applications, or other proprietary rights that MAY cover technology that MAY be required to practice this specification.

# Document History

   [[ To be removed from the final specification ]]

   -00 

   *  Initial version
