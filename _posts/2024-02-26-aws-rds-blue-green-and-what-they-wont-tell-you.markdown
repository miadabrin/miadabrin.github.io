---
layout: post
title:  "AWS RDS Blue Green And What They Won't Tell You"
date:   2024-02-26 20:45:33 -0500
categories: AWS RDS Blue/Green
---
# RDS Blue Green And What They Won't Tell You
RDS Blue Green is one of the most useful features that RDS team has created for their customers to be able to make chanages to their databases. Things including but not limited to, filesystem changes, version upgrades and schema changes (which I think is the most important feature). 
With all great things there is always a catch (a.k.a what can go wrong?) and RDS Blue Green is not an exception. There are a bunch of footguns that you need to prepare yourself for when opting in into using the feature

## Chapter 1: Replication lag
The first issue you need to be aware of when working with RDS Blue Green is the replication lag (This is assuming you are using EBS for your storage layer). once you create new green instances you will notice a non-ordinary increase in the replication lag of your instance. You will see something like this ( the graph will look different based on the volume of the tables, distribution of data, indices ,etc). 
![Replication Lag](/assets/images/ReplicationLag.png).

This is not really documented explicitly anywhere in RDS documentation but if you piece together different parts of the puzzle you will figure out the reason is that RDS streams your databases's blocks from s3 in the background (they call it lazy loading or hydration in different places) . There are some awesome [blog]((https://engineering.cred.club/lazy-loading-of-snapshot-restores-and-its-implications-on-database-performance-d866097b02fa) and) [posts](https://cintia.me/blog/post/lazy-rds/) that talk about the snapshot restoration and lazy loading which is the exact same things that is happening here.
