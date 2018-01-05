---
authors: George Pochiscan <george.pochiscan@sphs.ro>
state: draft
---

# RFD 2 Spearhead DNS Service (DNS)

## Overview

All our DNS services, Cloud DNS services and Hosting DNS service should be 
integrated and provide centralized management.


# What problem are we solving?

Redundant DNS and seamless DNS integration for SC and hosting services.

## Key Requirements

* DNS Security
* Fixed TTLs for all zones
* Geographic redundancy


The first principles we are looking at include:

* DNS Security
* Fixed TTLs for all zones
* Geographic redundancy

## How will users interact with these features?

Main interation will be performed via CLI. No web interface should be available.
Every client that creates in our cloud an instance with an external IP Address 
should have an DNS entry for that instance, that is created dynamic based on the 
IP Address (See AWS functionality at this moment)


Developers may in the future build upon this framework and integrate with other
services.

## What repositories are being changed, if known?

A new repository Spearhead/dns (or similar) will be created to host
configuration files (possibly other details) for the framework.

## What is the security impact?

If DNS is not available due to incorrect configuration, user error, server error, 
datacenter unavailability, network errors all services that depends on DNS will 
stop function properly ( web, e-mail, applications ). With redundancy those risks 
are minimalized.
