---
authors: Marius Pana <mp@spearhead.systems>
state: publish
---

# RFD 10 Spearhead Cloud Customer Portal feature updates

[Trixae](https://github.com/spearheadsys/sc-portal), our cloud customer portal, is in an MVP state: it offers minimum functionality for general operations with cloud resources (provision, start, stop, etc.). There are pieces of the software that also require some fine tuning in order for the product to become more usable and user-firendly/intuitive.

# What problem is this solving?

We are trying to break our dependece on the existing customer portal (my.spearhead.cloud) which is based on the Joyent provided piranha codebase. This codebase is old but more importantly we could not find developers/designers that would work with this codebase (based on angular v1) in order to update and maintain.

Our new portal will become the default and as such must offer a pleasant and stable experience.

# What are the principles and constraints on the design of the solution?

We have decided we would continue using Trixae for the forseeable future by adding new features, fixing existing issue/bugs and generally expanding it as requirements arise.

# How will users interact with these features?

Users will interact with this portal via their browser. Alternatively and for more advanced use cases, there is a full featured and mature API as well as command line interface.

Operators may use the portal to troubleshoot/investigate issues or for our own tenants. Generally operators will; use the CLI/API's however if we have customers permissions and credentials, we may use this portal.

Once we implement this RFD, the portal will be fully functional meaning we are not missing major functionalities. 


# What repositories are being changed

The following repositories will be modified/changed to accomodate our proposed changes.

[sc-portal](http://github.com/spearheadsys/sc-portal) otherwise nown as Trixae.


# What public interfaces are changing?

We are changing the UI of the customer portal. API and CLI continue to function as before.


# What is the upgrade impact?

For an existing install, we expect to git clone/pull the new resources, update configuration files and off we go. Downtime should be be minimal, requireing just a reboot of the service.
Because we can deploy multiple instances of the portal, we can bring up the new version and redirect trafic to the new once we are ready.
