---
layout: page
title: "Users"
tagline: "DataSHIELD Users Documentation"
group: navigation
---
{% include JB/setup %}

## Overview

* [DataSHIELD Administrator](#admin)
  * [Prerequisites](#serversetup)
  * [Usage](#adminusage)
* [DataSHIELD User](#user)
  * [Prerequisites](#clientsetup)
  * [Usage](#clientusage)

<a name="admin"> </a>
## DataSHIELD Administrator

As a DataSHIELD administrator, you are responsible for:
* installing DataSHIELD packages in R server,
* publishing DataSHIELD aggregation and assignment methods.

<a name="serversetup"> </a>
### Prerequisites

A Opal server has to be available.

See: [Opal Server Administrator Guide](http://wiki.obiba.org/display/OPALDOC/Opal+Server+Administrator+Guide)

The Opal server must be backed by a R server in which data will be pushed from Opal for being aggregated.

See: [Opal R Server Set Up](http://wiki.obiba.org/display/OPALDOC/Opal+R+and+DataSHIELD+User+Guide#OpalRandDataSHIELDUserGuide-ServersideInstallation)

<a name="adminusage"> </a>
### Usage

Opal provides a web interface for performing those administration tasks.

See:
* [DataSHIELD Packages Administration in Opal](http://wiki.obiba.org/display/OPALDOC/DataSHIELD+Administration#DataSHIELDAdministration-Packages)
* [DataSHIELD Methods Administration in Opal](http://wiki.obiba.org/display/OPALDOC/DataSHIELD+Administration#DataSHIELDAdministration-Methods)

You can also use R to administrate one or several Opal servers DataSHIELD configurations: *opaladmin* R package provides the Opal administration toolbox.

	install.packages('opaladmin', repos=c(getOption('repos'), 'http://cran.obiba.org'), dependencies=TRUE)

All the functions starting with `dsadmin.` are meant to administer DataSHIELD configuration. The following example installs a DataSHIELD-R package and publish its methods:

	# Login in Opal
	library(opaladmin)
	o<-opal.login('dsadmin', 'password', 'https://some-opal-host:8443',opts=list(ssl.verifyhost=0,ssl.verifypeer=0,sslversion=3))

	# Install dsbase package on R server
	dsadmin.install_package(o, 'dsbase')

	# Configure datashield methods in opal
	# Clean all methods
	dsadmin.rm_methods(o)
	# Publish dsbase package methods
	dsadmin.set_package_methods(o, 'dsbase')


<a name="user"> </a>
## DataSHIELD User

DataSHIELD users will connect to a set of Opals and perform some DataSHIELD analysis.

<a name="clientsetup"> </a>
### Prerequisites

R must be installed on the client side.

See: [Download and Install R](http://cran.r-project.org/)

A dataset harmonized with other datasets deployed in different Opal servers must have been uploaded. At least 'View dictionary and summaries' is granted to the user on the corresponding tables in each Opal server.

See: 
* [Import Data in Opal](http://wiki.obiba.org/display/OPALDOC/Working+with+Datasources#WorkingwithDatasources-ImportData)
* [Table Permissions in Opal](http://wiki.obiba.org/display/OPALDOC/Table+Details#TableDetails-Permissions)

<a name="clientusage"> </a>
### Usage

From a R console you will need to install the DataSHIELD client package you are interested in. For instance [dsbaseclient](https://github.com/datashield/dsbaseclient):

	install.packages('dsbaseclient', repos=c(getOption('repos'), 'http://cran.obiba.org'), dependencies=TRUE)

Windows users will have to explicitly install package dependencies.

See: [Opal R Client Set Up](http://wiki.obiba.org/display/OPALDOC/Opal+R+and+DataSHIELD+User+Guide#OpalRandDataSHIELDUserGuide-ClientsideInstallation)

Then follow instructions to perform DataSHIELD analysis within Opal.

See: [Opal DataSHIELD Usage](http://wiki.obiba.org/display/OPALDOCDEV/Opal+R+and+DataSHIELD+User+Guide#OpalRandDataSHIELDUserGuide-DataSHIELDUsage)
