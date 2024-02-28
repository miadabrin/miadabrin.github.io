---
layout: post
title:  "AWS RDS Blue Green And What They Won't Tell You"
date:   2024-02-26 20:45:33 -0500
categories: AWS RDS Blue/Green
---
# RDS Blue Green And What They Won't Tell You
RDS Blue Green is one of the most useful features that the RDS team has created for their customers to be able to make changes to their databases. This includes, but is not limited to, filesystem changes, version upgrades, and schema changes (which I think is the most important feature). With all great things, there is always a catch (a.k.a. what can go wrong?), and RDS Blue Green is not an exception. There are a bunch of pitfalls that you need to prepare yourself for when opting in to using the feature.

## Replication lag
The first issue you need to be aware of when working with RDS Blue Green is the replication lag (This is assuming you are using EBS for your storage layer). Once you create new green instances, you will notice a non-ordinary increase in the replication lag of your instance. You will see something like this (the graph will look different based on the volume of the tables, distribution of data, indices, etc.).
![Replication Lag](/assets/images/ReplicationLag.png).

This is not really documented explicitly anywhere in RDS documentation, but if you piece together different parts of the puzzle, you will figure out the reason is that RDS streams your database's blocks from S3 in the background (they call it lazy loading or hydration in different places). There are some awesome [blog](https://engineering.cred.club/lazy-loading-of-snapshot-restores-and-its-implications-on-database-performance-d866097b02fa) and [posts](https://cintia.me/blog/post/lazy-rds/) that talk about the snapshot restoration and lazy loading, which is what is happening here.

There are multiple things that you can do to speed this up, including running a mysqldump on your database (in most cases not really feasible as it will take a long time and will hit max_execution_time of your database) or creating a script to run select on your tables in ranges.

In most cases, the replication lag goes down quicker than the EBS hydration finishes (mostly because a large chunk of the data is untouched when doing the replication after the snapshot is restored). This is also dangerous since it means once you switchover to your green instances, you are going to have slow reads for a certain period of time until your customers have all accessed the hot parts of your database.

Also, as a side note, make sure you take a snapshot of the database before you start the blue/green. That can ensure your snapshot is new enough to be used and have less replication lag going forward to catch up with the newest changes.

### What you should do
The best approach is touching the hot part of your database beforehand on the green instances. Normally, that is the top 20% of the newest records of your database, but it is not always the same across all workloads. You will need to find out what is going to be accessed more often in your workload and be fine with some records being a bit slow to access for the first time (which is fine in most cases).

## Server Identity Change and breaking CDC tools
Tools like Debezium stream changes from your database to Kafka (or any other tool for that matter) and they depend on the GTIDs, server ids, and binlog positions to record where they are regarding streaming the binary log of your database.

New Green instances don't have the same server ids nor the same binary logs and positions. They use the current master's GTID set along with their own initiated GTID sets to distinguish the changes.

So when you make a schema change in your green database, that schema change is going to be reflected with a separate GTID set in the new green replica, for instance.

What it means at the end of the day is that you will need to do a couple of steps to ensure your CDC tool can keep track of the same changes on the new instances once they switchover. If you are using Debezium, you will need to do a few steps to reset the connector offsets.

1. Stop your connector and record its current offset.
2. Find the same position for that offset on the new server's binary logs.
3. Do the switchover / remove connect-offsets topic and reboot the connector in schema_only_recovery mode.
4. Let the connector start streaming from the new servers. Then stop it again and move the offsets to what you found in step 2. Restart the connector, and it will restream the changes.

Note that this can risk a few minutes of duplicated changes to be streamed changes, but that seems like a reasonable choice in most cases.

## Your app recognizing the read-only mode 
During the switchover, RDS stops writes but not reads. That means your database will be put in read-only mode for a period of time until the switchover completes. If your app doesn't know this, it might try to write records while that is the case, which might be troublesome in some cases. Most of the time, that should be okay, but this is something to keep in mind.


# Conclusion
RDS Blue Green is a great feature, but it can come with its own dark corners. If you have tried it and had issues, I would love to hear about it. Please don't hesitate to message me on LinkedIn.