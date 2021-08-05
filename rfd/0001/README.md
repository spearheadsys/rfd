---
authors: Marius Pana <mp@spearhead.systems>
state: published
---

# RFD 1 Spearhead Directory Service (LDAP)

## Overview

As we grow we require a central store of user ID's to use for authentication/
authorization purposes within our infrastructure and third parties
(integrations).

# What problem are we solving?

We use many different services (email, hosting, etc.) and more are coming. It is
cumbersome to maintain user/passwords and other access policies individually per
service. In many cases we end up with multiple user accounts/passwords and
managing the lifecycle of these accounts is difficult and error prone: when a
user leaves we must also track down all of the accounts and disable/delete those
as well.  

## Key Requirements

We wish to have a central location for all user authentication requests so that
we can easily create and manage users. We can then use this central store to
authenticate with all of our required services.

The first principles we are looking at include:

* A centralized store for obtaining user ID's and Passwords
* Group membership information
* Restricted access (RBAC)
* Secure end-to-end access

## How will users interact with these features?

Operators will interact directly (cli, web, clients) with the directory based on
their permission levels. Operations will include adding new objects, modifying
policies  and ACLs, deleting users, etc. All operations will be typical of other
LDAP based directory services.

End users will transparently interact with the system: users will receive their
credentials and will not have to manage any properties within the directory
itself.

Developers may in the future build upon this framework and integrate with other
services.

# Proposal

We have had generally a positive experience using ApacheDS. Initially we will setup a single master server running in spearhead.cloud, backed-up offsite (restoring is a matter of copuing some files and starting the service). In time we will add a Multi-Master replication in a geo-redudant fashion (or at least in more than one AZ).

We will store our user identities, groups and some systems (rundeck specifically). In time we may expand to include customer identidies and other details.

## What repositories are being changed, if known?

A new repository Spearhead/ldap (or similar) will be created to host
configuration files (possibly other details) for the framework.

## What is the security impact?

A compromised directory could allow an attacker access to sensitive information
or services. Furthermore a compromised directory could be used against us and
therefore other methods of access for critical situations must be implemented
(local accounts, override mechanisms, etc.). A mechanism to disable/invalidate
all accounts must be implemented.
A compromised user account impact depends on the privileges of the compromised
account. A mechanism to quickly disable any compromised account must be
implemented.
