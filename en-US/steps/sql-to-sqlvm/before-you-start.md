## Preparing for database migration

As you prepare for migrating your SQL Server database to SQL Server on Azure VMs, be sure to consider the versions of SQL Server that are supported and to address any prerequisites. This will help to ensure an efficient and successful migration.

**Important**: For scenarios in which you need to meet certain regulatory, policy, or compliance requirements that prevent you from using SQL Server on Azure VMs, you can use [Azure Stack](https://azure.microsoft.com/overview/azure-stack/). You can run Azure Stack at the edge for remote locations, run it completely disconnected from the internet, or create a hybrid solution.
The guidance in this scenario applies to migrations from SQL Server on-premises to SQL Server on Azure VMs as well as migrations to Azure Stack Virtual Machines.

### Overview

This scenario describes how to migrate a SQL Server instance to SQL on Azure Virtual Machines (VMs).

### Supported versions

SQL Server on Azure VMs supports migration of the following versions of SQL Server:

* SQL Server 2005
* SQL Server 2008 and SQL Server 2008 R2
* SQL Server 2012 and SQL Server 2012 SP1 CU2
* SQL Server 2014
* SQL Server 2016
* SQL Server 2017

### Overview of prerequisites

Before beginning your migration project, it is important to address the associated prerequisites.

* Download and install the latest version of the [MAP Toolkit](http://go.microsoft.com/fwlink/?LinkID=316883).
* Download and install the latest version of the [Database Experimentation Assistant](https://www.microsoft.com/en-us/download/details.aspx?id=54090).
* Download and install the [Data Migration Assistant](https://www.microsoft.com/download/details.aspx?id=53595) v3.3 or later.
* Create an instance of SQL Server on Azure VMs by following the detail in the article [How to provision a Windows SQL Server virtual machine in the Azure portal](https://docs.microsoft.com/en-us/azure/virtual-machines/windows/sql/virtual-machines-windows-portal-sql-server-provision).

### Additional resources

* See the white paper [Choosing your database migration path to Azure](https://aka.ms/dbmigratewp) for additional information and recommendations.
* For a matrix of the Microsoft and third-party services and tools that are available to assist you with various database and data migration scenarios as well as specialty tasks, see the article [Service and tools for data migration](https://docs.microsoft.com/azure/dms/dms-tools-matrix).

**Videos**

* For an overview of the Azure Database Migration Guide and the information it contains, see the video [How to Use the Database Migration Guide](https://azure.microsoft.com/resources/videos/how-to-use-the-azure-database-migration-guide/).
* For a walk through of the phases of the migration process and detail about the specific tools and services recommended to perform assessment and migration, see the video [Overview of the migration journey and the tools/services recommended for performing assessment and migration](https://azure.microsoft.com/resources/videos/overview-of-migration-and-recommended-tools-services/).
