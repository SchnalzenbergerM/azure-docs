---
title: Limitations in Azure Database for MySQL  | Microsoft Docs
description: Describes preview limitations in Azure Database for MySQL.
services: mysql
author: jasonh
ms.author: kamathsun
manager: jhubbard
editor: jasonwhowell
ms.service: mysql-database
ms.topic: article
ms.date: 01/11/2018
---
# Limitations in Azure Database for MySQL
The Azure Database for MySQL service is in public preview. The following sections describe capacity, storage engine support, privilege support, data manipulation statement support, and functional limits in the database service. Also see [general limitations](https://dev.mysql.com/doc/mysql-reslimits-excerpt/5.6/en/limits.html) applicable to the MySQL database engine.

## Service tier maximums
Azure Database for MySQL has multiple service tiers to choose from when creating a server. For more information, see [Understand what’s available in each service tier](concepts-service-tiers.md).  

There is a maximum number of connections, Compute Units, and storage in each service tier during preview, as follows: 

|                            |                   |
| :------------------------- | :---------------- |
| **Max connections**        |                   |
| Basic 50 Compute Units     | 50 connections    |
| Basic 100 Compute Units    | 100 connections   |
| Standard 100 Compute Units | 200 connections   |
| Standard 200 Compute Units | 400 connections   |
| Standard 400 Compute Units | 800 connections   |
| Standard 800 Compute Units | 1600 connections  |
| **Max Compute Units**      |                   |
| Basic service tier         | 100 Compute Units |
| Standard service tier      | 800 Compute Units |
| **Max storage**            |                   |
| Basic service tier         | 1 TB              |
| Standard service tier      | 1 TB              |

When too many connections are reached, you may receive the following error:
> ERROR 1040 (08004): Too many connections

## Storage engine support

### Supported
- [InnoDB](https://dev.mysql.com/doc/refman/5.7/en/innodb-introduction.html)
- [MEMORY](https://dev.mysql.com/doc/refman/5.7/en/memory-storage-engine.html)

### Unsupported
- [MyISAM](https://dev.mysql.com/doc/refman/5.7/en/myisam-storage-engine.html)
- [BLACKHOLE](https://dev.mysql.com/doc/refman/5.7/en/blackhole-storage-engine.html)
- [ARCHIVE](https://dev.mysql.com/doc/refman/5.7/en/archive-storage-engine.html)
- [FEDERATED](https://dev.mysql.com/doc/refman/5.7/en/federated-storage-engine.html)

## Privilege support

### Unsupported
- DBA role
Many sever parameters and settings can inadvertently degrade server performance or negate ACID properties of the DBMS. As such, to maintain our service integrity and SLA at a product level we do not expose the DBA role to customers. The default user account, which is constructed when a new database instance is created, allows customers to perform most of DDL and DML statements in the managed database instance. 
- SUPER privilege 
Similarly [SUPER privilege](https://dev.mysql.com/doc/refman/5.7/en/privileges-provided.html#priv_super) is also restricted.

## Data manipulation statement support

### Supported
- LOAD DATA INFILE - Supported, but it must specify the [LOCAL] parameter that is directed to a UNC path (Azure storage mounted through XSMB).

### Unsupported
- SELECT ... INTO OUTFILE

## Preview functional limitations

### Scale operations
- Dynamic scaling of servers across service tiers is currently not supported. That is, switching between Basic and Standard service tiers.
- Dynamic on-demand increase of storage on pre-created server is currently not supported.
- Decreasing server storage size is not supported.

### Server version upgrades
- Automated migration between major database engine versions is currently not supported.

### Point-in-time-restore
- Restoring to different service tier and/or Compute Units and Storage size is not allowed.
- Restoring a deleted server is not supported.

## Functional limitations

### Subscription management
- Dynamically moving pre-created servers across subscription and resource group is currently not supported.

## Current known issues
- MySQL server instance displays the wrong server version after connection is established. To get the correct server instance versioning, use select version(); command at the MySQL prompt.

## Next steps
- [What’s available in each service tier](concepts-service-tiers.md)
- [Supported MySQL database versions](concepts-supported-versions.md)
