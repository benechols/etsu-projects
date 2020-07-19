# ETSU Projects
Descriptions of some of the various projects created and maintained in my role as a Senior Software Engineer for East Tennessee State University. This is just a small subset of the 29 custom built websites currently running in C# .NET 4.x and 30 services running mostly in .NET Core (2.x & 3.x) but a few still on .NET 4.x and a few in Python. On most of those I am the full stack developer including any and all requirements gathering all the way through long term support. All websites utilize the ASP.NET Razor engine, jQuery, Bootstap and a host of other 3rd party javascript libraries. The goal is to create all sites to work as simply and as error free as possible so that training can be kept to a minimum and that everyone who might use them should be able to without any questions. Some sites I've created are used heavily by every employee and student. Future plans include migrating the .NET 4.x sites to .NET 5 next year upon its first LTS release.


## Identity Management
A full-fledged identity management solution. This takes data from the ERP in Oracle and in turn creates / updates / deletes accounts. There are several roles that a user can be such as Applied, Faculty, Alumni, etc. Each role is granted different permissions and has different properties. In addition to giving access it is just as important to remove access when a user changes role or if an employee changes department. This consists of a Processes which are collection of Subprocesses. A process might be Update / New / Returning / etc. The subprocesses are the individual tasks related to a specific action such as creating the Active Directory account or issuing a license within Azure. There are over 60 subprocesses across the following areas:
  
  * Azure (Microsoft 365)
  * Active Directory
  * Banner ERP (Oracle database)
  * File Shares
  * Exchange
  * Custom APIs

Most calls are done through provided libraries or APIs but some tasks within Azure and Exchange can only be completed with Powershell. All tasks are fully logged so at any point a history of every task performed upon a user can be retrieved. The system also auto retries, with delays, tasks for issues such as service outages and only bubbles up errors after multiple failures. Management of most of the access a role is granted is handled in an accompanying site. There bulk tasks can also be performed on everyone within a role in case of new permissions granted.


## Data API
We have multiple services that need to consume general data through an API be it employee and student data and pictures, course information, etc. This is a RESTful WebApi project that employees HMAC security on calls as well as Swagger definitions.


## Website Administration
A one stop shop to manage all of our custom sites from security and logging to forms and workflows. This one site works for all of our environments at the same time.


## ETLs
When I entered the position, I had to maintain about a dozen different SSIS packages within SQL Server 2008. These were all replaced with C# dotnet core services running in AWS Lambda. Most of which are controlled by cron schedules. They run just as fast as the SSIS package did with proper multithreading of tasks that can be run in parallel. These move data between Oracle <-> SQL Server, Postgres <-> SQL Server, and Oracle <-> Postgres. The programming is simple and easy to follow.


## Core Library
All websites utilize a core library of functionality to reduce the need for duplicate coding. As monolithic libraries are largely a thing of the past due to the several obvious drawbacks my next main goal is to break it out into microservices. Time constraints are an issue and the only one I have tackled thus far is Logging which brought a 5x performance increase within applications when simply writing a log. This is available as an internal NuGet repository that I set up. It handles all the common tasks needed for most sites such as:
  * Authentication & Security
  * Email, Twilio, Slack
  * Files (S3)
  * Forms & Workflows
  * Logging
  * Settings
  * etc


## Website Template
I created the template project when I started working at ETSU as the group did not have one and every programmer's websites had different base functionality and look and feel. The template is not only a starter template available within Visual Studio but also a NuGet package so any updates or new functionality can be rolled out to any existing site with a simple package update. This contains all of the basic work needed to get a new site up and running such as authentication pages, settings for admins, global error handling, etc. This allows simple one-page sites to be created in less than an hour or so depending on the complexity of the new site.


## Workflows
Everyone makes a workflow engine and so did we. Workflows are created in an easy to use UI with complex step and assignment rules, decision hierarchies, and sub workflows. Code is auto generated for use in projects. While the university has access to other types of forms and workflows they tend to only be used on simpler tasks and ours is reserved for those with complex requirements.


## Advisories
A campus advisories system. A rather simple site that has alerts of various levels of severity. Aside from the standard management and display site, the advisories are available via SOAP, JSON, or RSS. Additionally, a service running through AWS API Gateway exists to consume CAP XML calls from a 3rd party vendor that also creates alerts.


## Electronic Timesheets
An electronic timesheets system with a full approval system including backups and proxies, instant and delayed notification and reminders. Feeds the Ellucian Banner ERP with data at the end of each pay period. Calendar is a customized Toast UI implementation. The university already owns an electronic timesheets system with the ERP but I was still tasked to create one that worked better for the needs of the university.


## Self Service Password Reset
A self-service password reset page backed by 2FA. Also heavily used by the University's Help Desk to view information on many users calling in for assistance.
