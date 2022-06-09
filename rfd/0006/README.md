
# RFD 4 Spearhead Cloud Customer Portal

## Overview
The existing piranha portal is still quite useful for operating your cloud resources as a tenant. It is however showing its age and updating / managing the current version was not an option for as we could not find angular1 experts.

# What problem are we solving?
Designing a new customer portal for tenants to access their cloud resources that would be able to handle the next 3 - 5 years of development (i.e. technology is still managed/manageable).

## Key Requirements
Create, delete machines, networks, users, roles and policies.
A more user-friendly experience.

## How will users interact with these features?
Via the web interface.


## What repositories are being changed, if known?
[sc-portal](https://github.com/spearheadsys/sc-portal)


## What is the security impact?
We are reusing http-signatures and the existing SSO authentication framework. 
