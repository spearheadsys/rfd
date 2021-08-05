---
authors: Marius Pana <mp@spearhead.systems>
state: abandoned
---

> spearhead.cloud currently utilises its own implementation of mantav1. Because upstream is no longer focusing on v1 of manta and the compute features we were interested in are no longer available we are abandoning our current object storage in favor of:
> 
> 1. Veeam backup & replication for BaaS, DRaaS, etc.
>
> 2. AWS s2, Azure Files/Object and miniio for customers looking for a local (to our cloud) object store

# RFD 3 Spearhead Cloud object storage 

## Overview

Currently we are using Joyent MANTA for object storage, specifically for backup purposes. While this works and is a very unique and interesting solution it is located in US-EAST which presents two distinct and specific issues:

* GDPR concerns as we would require complex contracts with Joyent and more specifically with our customers so that they accept hosting outside of the EU
* performance issues while uploading large files. Uploading 800GB is not a pleasant experience for our customers as it often fails and it must be restarted


# What problem are we solving?

tbd

## Key Requirements

* object storage
* support for Linux, Windows (macos and others may be of future interest)

The first principles we are looking at include:

* tbd

## How will users interact with these features?

tbd - sph will work with customers 


## What repositories are being changed, if known?

A new repository Spearhead/..will be created to host... tbd

## What is the security impact?

tbd
