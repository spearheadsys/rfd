---
authors: Marius Pana <mp@spearhead.systems>
state: pre-draft
---

# RFD 10 Spearhead Cloud Customer Portal feature updates

[Trixae](https://github.com/spearheadsys/sc-portal), our cloud customer portal, is in an MVP state: it offers minimum functionality but not much else. There are pieces of the software that also require some fine tuning in order for the product to become more usable, more user-firendly/intuitive.

# What problem is this solving?

We are trying to break our dependece on the existing customer portal (my.spearhead.cloud) which is based on theJoyent provided piranha codebase. This codebase is old, not very intuitive but most importantly we could not find developers/designes that would work with this codebase (based on angular v1) in order to update and maintain.

Our new portal will become the default and as such must offer a pleasant and stable experience.

# What are the principles and constraints on the design of the solution?

You should use this section to describe the first principles or other important decisions that constrain the problem. For example, a constraint on the design may be that we should be able to do an operation without downtime.

# How will users interact with these features?

Here, you should consider both operators, end users, and developers. You should consider not only how they'll verify that it's working correctly, but also how they'll verify if it's broken and what actions they should take from there.

What repositories are being changed, if known?

If it's known, a list of what git repositories are being changed as a result of this would be quite useful.

What public interfaces are changing?

What interfaces that users and operators are using and rely upon are changing? Note that when changing public interfaces we have to be extra careful to ensure that we don't break existing users and scripts.

What private interfaces are changing?

What interfaces that are private to the system are changing? Changing these interfaces may impact the system, but should not impact operators and users directly.

What is the upgrade impact?

For an existing install, what are the implications if anything is upgraded through the normal update mechanisms, e.g. platform reboot, sdcadm update, manta-adm update, etc. Are there any special steps that need to be taken or do certain updates need to happen together for this

What is the security impact?

What (untrusted) user input (including both data and code) will be used as part of the change? Which components will interact with that input? How will that input be validated and managed securely? What new operations are exposed and which privileges will they require (both system privileges and Triton privileges)? How would an attacker use the proposed facilities to escalate their privileges?



> Trixae MVP is in production at https://t.spearhead.systems
>  we are now targeting a more featurefull version
>
> things we would like from Trixae
> * extremely simple to use
> *volumes
- show more details (such as ip and mount point)
- enable some form of pagination, the list can get big for large customers and unmanageable

firewall
- enable some form of pagination, the list can get big for large customers and unmanageable
- filter by vm name (rules are attached to vms as far as I know)

machines
- enable some form of pagination, the list can get big for large customers and unmanageable
- add list of firewall rules
- add possibility to add new firewall rules (delete, etc.)


dashboard
- introduce a new entry point, the default page, which is a dashboard containing
- different statistics and metrics such as
    - usage trend
    - number of running, stopoed, etc vms
    - number of volumes
