---
authors: Marius Pana <mp@spearhead.systems>
state: predraft
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
we can easily create and manage users.

The first principles we are looking at include:

* A centralized store for obtaining user ID's and Passwords
* Restricted access (RBAC)
* Secure end-to-end access

## How will users interact with these features?

Operators will interact directly (cli, web, clients) with the directory based on
their permission levels. Operations will include adding new objects, modifying
policies  and acls, deleting users, etc. All operations will be typical of other
LDAP based directory services.

End users will transparently interact with the system: users will receive their
credentials and will not have to manage any properties within the directory
itself.

Developers may in the future build upon this framework and integrate with other
services.

## What repositories are being changed, if known?

A new repository Spearhead/ldap (or similar) will be created to host
configuration files (possibly other details) for the framework.

## What is the upgrade impact?

Since this is an initial deploy it will require creating the directory, integrating it with our services (email, git, mattermost, etc.) and then assigning the new uid's.

## What is the security impact?

The service itself must be secured end-to-end (starttls/ssl/tls) including the operating environments. The service itself will require fine grained controls (RBAC/ACLs) to limit what users can modify within the directory.
A compromised directory must be handled in an automated fashion and mechanisms for limiting impact as well as service restoration to a known state must be available.
