# microsoft-ignite-2019
Stockholm April 2019  

## Sessions
### Azure fundamentals
FUN10 - Discover Microsoft Azure  
FUN20 - Azure networking basics  
FUN30 - Discovering Azure tooling and utilities  
FUN40 - Azure security basics  
FUN50 - Storing data in Azure  

### Operating applications and infrastructure in the cloud
SRE10 - Modernizing your infrastructure: moving to Infrastructure as Code  
SRE20 - Monitoring your infrastructure and applications in production  
SRE30 - Diagnosing failure in the cloud  
SRE40 - Scaling for growth and resiliency  
SRE50 - Responding to and learning from failure  

## Day 1
### Discovering Azure
https://portal.azure.com

MS Cloud computing platform
Biggest advantage.. More cost effective, pay for what you use
Allows dev to focus on developing applications
More reliable
Security (physical, digital)

Styles of cloud
Public - Most common, AWS, MS, Google
Highly scalabe pay as you go
Private - Azure stack.  Cloud environment in your data center
Disadv - Purchase and maintain hardware, require skilled IT personnel
Hybrid - Private + Public.  Adv: Keep systems running on out of date hardware.  Reliability on running locally, higher availability.  DisAdv - may be expensive, more complicated to set up.

IaaS - Infra as service.  Control of hardware.
PaaS - Build test and deploy software. Don't worry about infra cost.
SaaS - Software centrally hosted and managed.  Monthly or yearly subscription.  Office 365 is an example.  Gmail, etc.

Cloud computing Services
Compute
Storage - Object storage
Applications - NoSQL and SQL database
Networking - Virtual networks
Analytics - Telemetry, Performance data

Azure main areas - Compute, networking and storage.  Security and management.
Azure compute services
	- Azure Virtual machine
	- Azure Kubernetes
	- Azure Functions

Azure networking services
	- Azure virtual network
	- Azure Load balancer
	- Azure traffic manager

Storage services
	- Blob, File, Table (NoSql)

Azure Active Directory
	- AD multi-tenant
	- Used by Azure and Office 365
	- Contains all identities of users in organisation
	- Centralised directory store

aka.ms/azure-portal tutorial

Azure Resource Manager (ARM)
Resource - Manageable item in Azure like VM
Resource group - Container that holds resources
Resource provider, service that supplies resources, Microsoft Computer, Microsoft Storage, 
Microsoft Web
Resource manager template - ARM template.  JSON that defines resources to deploy to a resource group.
Subscriptions, resource groups and resources

Compute options
	- Memory, cpu, nvidia GPUs, skylake processors, etc. Lots of options
Virtual machines
	- Software emulation of physical computer.  VM hosts an OS.  Has virtual processor, memory, storage, networking.
	- AKS fully managed kubernetes cluster

Serverless
Microsoft Flow - built on logic apps, simple integrations, for non tech employees
Logic Apps - Advanced flow for devs
Functions - serverless, small piece of code, c# javascript f# java typescript, integrates with azure services, functions runtime is open source
App Service webjobs - runs scripts

### Azure networking basics
Security should be part of your strategy from the beginning

Virtual network connects vm to vpn
	- Create private networks in the cloud with full control over IP addresses, DNS servers, security rules and traffic flows
Naming: All azure resources have a name. Name must be unique within a scope, but that can different for each resource type.  Virtual network names must be unique within a resource group but can be duplicated between a subscription or Azure region.  Define and use a consistent naming convention so that it is easier to manage resources as you grow your network, e.g. by project or location.
Region: Azure data center within a specific geographic location.  Resources are created in an azure region and subscription.  Resource can only be created in a virtual network that exist in the same region and subscription as the resource.  You can connect virtual networks that exist in different subscriptions and regions.
Subscriptions: Deploy as many virtual networks as required within each subscription up to the limit.  Can craete multiple virtual networks per subscription per region and you can craete multiple subnets withing each virtual network.
	
Load balancer balances inbound and outbound connections
Traffice manager

Connectivity
Virtual network to Virtual network (Vnet peering) - connect two azure virtual networks.  Now they will appear as one for connectivity purposes. Vnet peering connects vnets within same azure region, Global vnet peering connects vnets across azure regions.
Each virtual network regardless of whether it is peered with another virtual network can have its own gateway.
VPN connecctions - hybrid networking scnearios.  Point to site, Site to site, and private site to site (express route)
Site to site vpn to azure vnet (vpn gateway) - vpn gateway is a virtual private gateway that is used to send enccrypted traffice between an azure virtual network.
Express route - create private connectiosn between azure data centers and infra on your environment.  Not over the public internet.

VPN gateway easier to configure and uses existing internet connection.  Routes through public intenet. 1 gig per sec.
Express route, up to 10 gigabit per sec.  Direct, private connection from wan to microsoft services.
Pricing depends on service you choose.
You can use them together.  E.g vpn gatewat as failover for express route

IP addresses
Public - to comm. With internet, including azure public facing services.
Private - allow comm within azure virtual network, on prem network, when you use a vpn gateway or expressroute.

DNS hostname resolution
Public IP address - specify a DNS domain name label for a public IP resource, creating a mapping for domainnamelabel.location.cloudapp.azure.com to public IP address in Azure managed dns services
Private IP address - All vms are configured with azure managed dns servers by default.

Resilient distributed data
Regions - 42 regions. Set of data centers deployed within latency defined  perimeter and connected through a dedicated regional low-latency network.  Additional plans for 12 regions.
Availability zones are physically sepearated locations within an Azure region.  Each AZ is made up of one or more datcentes equipped with independent power, cooling and networking.

Azure CDN offers devs a global solution for delivering high bandwidth conect to users by catching their content strategically at diff locations around the world.  Offers dunamic site acceleration, CDN caching rules, HTTPS custom domain support, geo giltering, file compression and diagnostic logs.  Offers cdn standard from microsoft, cdn standard from akami, cdn standard from verizon, cdn premium from verizon.

Security
1.Filter traffic: Network security groups
With NSG, multi tier application architectures can be hosted in Azure

2.Network virtual applicances: VMs that perform specific network functions. Scenarios: It policy and complaince, consistency between on prem and Azure.  Supplement/complement Azure capabilities.

Routing traffic
1.BGP rules border gateway protocol.  Enables transit routing.  Full mesh redundant paths

What is availability and high availability?
How long is service running without interruption?  5 9s of availability = 99.999
Resiliency - ability to recover from failures and continue to function.  Responding to failures in a way that avoids downtime and data loss.
Distaster recovery: Ability to recover from rare, but major failures.
High avail: Ability for an app to conute running ina  healthy state without significant downtime.

Azure load balancer:  Scale apps and create high availability and resiliency for your services and applications.  Public lb maps public IP address and port number of incoming to private IP address and port number of the VM and vice versa.  Reconfigures itself as you scale instance up or down.  Outbound connections (SNAT) all outbound flows from private IP adress from your virutual network to public ip address on the internet can be translated to a frontend ip of the load balancer.
Internal lb directs traffic obly to resources that are inside a virtual network or that uses a vpn to access Azure infrastructure.  Common to use in multi tier application.

Azure appllication gateway, web traffic load balancer that enables you to manager traffic to your web apps.
Scalable, web application firewall, SSL offloading (https is slow, so this can save you compute cycles), integrated with other azure services.

Azure availability zones - fault isloated locations withing an azure region.  4 9s of reliability.

Azure traffic manager - DNS based traffic load balancer that enables you to distribute traffic optimally to services across global Azure regions.  Global dns load balancing, auto failover when endpoint goes down, combine with hybrid apps. Distribute traffic for complex deployments.

Azure Front Door (Only 2 weeks old, now in GA)
Global http load balancing.  Provides scalable and secure entry  point for fast delivery of your global web applications. SSL offloading, app. Accelberation, global http load balancing with instant failover.  Front door only supports HTTP acceleration.

You can use front door and traffic manager (dns level) together.

### Azure tooling
- Command line (Azure CLI and Powershell modules for Windows, Powershell core)
- VS Code (lots of languages supported, Azure extension allows you to deploy to Azure, Liveshare extension, Markdown extension, Spelling extension)
- Azure Cloud Shell, in browser based shell.  Need to log into Azure.  Put things in cloudrive if you want to save your files.
- Azure Resource Manager templates (JSON , parameters)

### Azure security basics
Azure security center collects data from everything in the cluster
http://aka.ms/5-things-lesson

Security is everyone's job.
Data breaches, insider threats, cryptojacking, accidental, corporate espionage, ransomware, DDoS, reputation

Cloud native: set of apps and services that automate and integrate the concepts of continuous delivery, microservices, containers and serverless.
Cloud security is different and better.  Complete infra visibility.  Complete threat monitoring.
Monitoring of everything with automated responses.  
http://aka.ms/Azure-Playbooks  
Automation of security in the SDLC.  Secure Software Dev Lifecycle.  
http://aka.ms/SSDLC  
JIT access control.  
http://aka.ms/Just-in-Time  
Automating patch management  
http://aka.ms/patch-management  
Resiliency: Means you have availability (CIA triangle: Confidentiality, Availability, Integrity)
Less heroics = happier staff

Azure security center: Unique intelligence, machine learning, threat intelligence, behavior analytics.  
http://aka.ms/Intelligent-Cloud  
The Cloud effect, learning from clouds.  
Shared responsibility: http://aka.ms/Intro-to-Sec  

Advanced threat protection: for your data
Assess potential vulnerabilities across Azure SQL and Storage services.
Classify and audit access to sensitive data in Azure SQL

IAM
Role based access control (RBAC)
Least privilege: Giving everyone exactly how much access and control they need but nothing more.
RBAC in Azure
http://aka.ms/Azure-IAM

JIT limits exposure to brute force attacks.  Reduce access to VM ports only when it is needed with JIT access.  Security centre - Advanced cloud defence - JIT vm access

HTTPS everywhere
Risk of not using HTTPS.  Modern browsers will alert users that the site is not secure.
Leaving you vulnerable to man in the middle attacks.
Something sniffing the traffic can see your requests and responses.
Makes you vulnerable to cryptomining. BeEF, browser exploitation framework.
Forcing HTTPS - Select an app in the dashboard - Settings - SSL settings or Custom domains

Azure key vault
http://aka.ms/Key-Vault

Azure Security Center recommendations
Security Centre - Overview - Threat Protection

Summary:
Turn on Azure Sec Center
Turn on Threat protection
Follow ASC recommendations
Implement JIT
Force HTTPS
Assign assess control to diff users
Benefits of cloud effect

### Storing data in Azure
Why cloud storage?
Database always available.  Access data via API.  Different strategies of storing data.

Data storage vs On-prem
Cost effectiveness
Reliability: Require backup, load balancing, disaster recovery
Storage types

Storage options
Blob: Object storage access via REST (Streaming and random object access scenario)
Files: File storage access via SMB, REST (lift and shift scenario)
Queues: Reliable messaging via REST (64 kb in size, scheduling async tasks)
Tables: NoSQL storage access via REST (key value storage)
Disks: IaaS VM VHD/disks access via REST (persistent disk for VMs)
All are built on a unified distributed storage system

Encryption
By default eveyrthing is encrypted.  Azure storage service encryption automatically and transpartently encrypts data before persisting it.

Redundancy and replication
LRS: Local redundant storage (3 replicas 1 region)
GRS: Geo redundant storage (6 replicas 2 regions (sometimes 3 regions))
RA-GRS: Read access - geo redundant storage (GRS + read access to secondary)
ZRS: 3 replicas across 3 zones, zone redundant storage

Create storage account in Dashboard.

CosmosDB
Supports SQL, Cassandra, MongoDB, etc.
Global distribution - high availability
Low latency anywhere in the world
Dashboard - Azure Cosmos DB
Azure data explorer allows you to work with data locally.  Works with azure storage also.

Azure SQL database
Migrate SQL server database without changing your app
Azure SQL database is a fully managed relational cloud database
Accelerate app dev and simply maintenance using SQL tools

SQL database with ML services.  Integrates with R analytical engine.  Good for data scientists and DBAs.  Operationalise ml scripts and models directly.
How to easily migrate and get benefits of cloud?  Assess - Migrate (Rehost (lift and shift), Refactor. Rearchitect, Rebuild - Optimise
What is SQL database managed instance?
Fully-managed service, SQL server compatibily, Full isolation and secure, new purchasing options.  Allows friction-free migration of SQL server workloads to a fully-managed service.

Accelerating journey to the cloud
Azure database migration service
PostgreSQL and MySQL on Azure.  4 9s of SLA.
Azure SQL data warehouse, scales up to petabytes of data.  Parallel processing.  Instant on compute scales in seconds.
Azure Data Factory - Hybrid data integration at a global scale.  Create, schedule and monitor data pipeline.  ETL service in the cloud.

Summary on why to move data to the cloud
Scalability, reliability, simplicity, built in intelligence, fully managed, global availability.
http://aka.ms/learn-storage   

## Day 2
### Modernising your infrastructure: Moving to Infra as Code

DevOps: Principles around people working in silos.  Ideation to production.
Culture, Automation, Lean, Measurement and Sharing.  (CALMS)  Automate everything that you possibly can.  Lean, don't overcomplicate, don't overarchitect.
Software Reliability Engineering.
Integrating DevOps.

SRE: How to deploy and maintain
In the cloud it rains!
Devoted to helping organisations achieve the appropriate level of reliability in their systems, services and products.
100% reliability is unreachable, expensive and reactive. 5 9s is 5.26 mins of downtime in a year. 4 9s is 52.56 minutes.
Sustainably achieve appropriate level of reliability in their systems, services and products.
Toil is manual repetitive work.

You can run VS code in cloud shell!
Command: code .

The ARM (Azure Resource Manager) template feeds into CI/CD part.
CI integrating development work into releasable chunks multiple times a day.
CD deploy automated releases.  Releases deployed automatically after pipeline is run and no problems are identified.

Caveats: Cannot deploy CosmosDB with ARM template.  

http://aka.ms/MyMSIgniteTheTour  

### Monitoring your infrastructure and applications in production
SRE is also about software engineering.
You don't want 5 9s, but an appropriate reliability level.
Why monitor?
Are my apps and infrastructure doing what I expect?  Are my apps and infrastructure doing what others expect?
Goals.  Are we heading in the right direction?
Change.  Systems are always changing.  Even if we aren't pushing out code change.  Are our systems healthy?  Are they being used as expected?
Look up Mickey Dickerson's hierarchy of reliability
Monitoring helps you with good observability.

Service Level Indicators (SLIs)
Reliability  
Availability: Can my system respond when I ask  
Latency:  Is system responding in appropriate amount of time  
Throughput: Vol of data from one point to another  
Coverage:  Can it cover all the data  
Correctness:  Did it do what it's supposed to do?  
Fidelity:  Netflix has good fidelity.  Netflix in the browser, if search wasn't working, then that part is turned off but you can still use Netflix.  
Freshness:  Is data served correctly.  
All of the above has to be from the customer's perspective.  

And sometimes that gets a bit hard.

SLIs are a ratio/proportion and HOW  
Number of successful HTTP calls / # total HTTP calls (as measured by the load balancer)  
Number of ops completed < 10 m / # of operations (as measured by the client)  
Number of records processed / # total records  
…  
Finding some sort of ratio

Where to get numbers from?
Reported by a server, reported by clients (browser), reported by the application, reported by the front end (load balancer, edge), closer to the users the better the experience
Reported by monitoring/testing infrastructure.

50 successful HTTP calls out of 100 HTTP calls
Ratio of 0.5 (50/100)
0.5 * 100
50% of availability
You will never get 100% of http calls.  Lots of ways to lose calls.

Where do the numbers come from?
There is no "right way", no best practise to determine this
You have to decide the right SLI.  And what is the thing that people want?
Understand the tradeoffs.
Example
How many requests came to the server?
How many errors came to the server?
But this does NOT include packets that never got to the server.  So you cannot do the math on this.  So if you only get logs from the server you may never see the full picture.

Azure Monitor
https://aka.ms/SRE20-Monitor
Dashboard - Logs - Application Insights
KQL used

Service Level Objectives (SLOs)
What is the line in the sand?

Where should we start?
User (Get as close to the user as possible!  Monitoring efforts should be moved as close to the user.  Because the bigger picture begins here.)
|
Load balancer
|
Web & app servers (NOT here)
|
Database

Basic SLO recipe
What are we measuring.. The thing?  HTTP requests, storage checks, operations
SLI proportions.  Successful 50% of the time
Time statement.  In the last 10 min period, during last quarter

Two ways to make SLO more complex
Compound
95% of reads last week took place in < 10 ms (as reported by disk checker)
95% of reads last week took place in < 20 ms (as reported by disk checker)
Segmented
Percentile of things (50, 60, 80, etc)

How to determine if something is a good SLO
Customer expectations
	- External and internal
"Some other data"
Current
"beware of the box" don't paint yourself in a box.. Don't spend efforts in maintaining a high SLO on things that may not need a high SLO

Look at the SLO and then determine when you want to be involved?  When it is below 85?  For example.  Then decide what you want to do.
What are users feeling about this?

Actionable Alerting
Alerts are NOT:
  logs, notifications, heartbeats, normal
You want an alert where you can do something about it. i.e. actionable
Needs a human to investigate and ideally resolve, the right person.  Remember humans are not automation.  If you can fix it then automate it.  Make it simple and easy for people to respond.

Crucial details:
Where is the alert coming from?
What expectation was violated?
Why this is an issue (for the customer)?
Steps to resolve the problem (or at least a specific pointer)
Create Actionable alerts

Future possible directions
Integrating multiple monitoring services
Modular monitoring
Aggregate monitoring
Correlate and anomaly detection
Monitoring the monitoring

SRE20-SRE30

### Diagnosing failure in the cloud
What is available to you to see what is breaking in the system etc.

See the slide for architect diagram.

Lifecycle of an incident
Detection - Response - Remediation - Analysis - Readiness

You will never prevent failure In a system, cannot avoid problems altogether.  But we can shorten phases of the lifecycle.

What do you mean by "wrong"?
-Not meeting objectives
-From the customer's perspective
SLI - indicator
SLO - objective (If it goes below then we have to get involved)

Detection
	1. Social media/phone calls/tickets/email
	2. Azure monitor/other monitoring (SRE20) (This is the better way obviously)
Actionable alerting
Heartbeats are bad practice, we want to be told when something is NOT up.  We want things which are actionable.
Crucial details:
Where the alert is coming form
What expectation was violated
Why is this an issue for the customer

Building for operational awareness in the cloud.  Build a system that is more observable.

Don't wait!  Do it now!

Azure toolbox consists of:
Azure monitor
Service health checks
Azure resource health
…

Is it the platform?  Check in Service health.
Create an alert for each different type of service as best practise.  Not one that covers many alerts.

Creating the perfect health alerts
It depends!
But guidance is don't create too many or too few.  Make sure alerts don't overlap.  Alert on production services preferentially.  Create them for people first so they know what to do.  Separate alerts for issues, maintenance and advisories.

Application map tool

Tools for troubleshooting
Diagnostic logs
Live debugging via log streaming
Log analytics

Kausto Query Language (KQL)  
Queries start with a table  
Some examples
Request
| take 10

Future directions
Observability: OpenCensus
Anomaly detection

Logstream

### Scaling for growth and resiliency
No purchasing lag now you don't need to wait to get more metal

What is the maximum capacity?
Do we need to scale our application?
And the underlying infrastructure?
Maybe
Why?  Buggy?  Applications are buggy, have memory leaks, etc.  Is this temporary?  Do I have unused capacity?
Anticipated load vs unexpected load

"Slow is the new down"

Necessity for scaling
	- Resource exhaustion under load (Managers look at the bottom line not what is needed)
	- Application/infrastructure ceases to meet its objective

Two train of thoughts
Scaling up (vertical) - risk of rebooting the machine and getting downtime.  If you do this during the maintenance window maybe it's alright.
Scaling out (horizontal) - adding more hosts to the load.  Do manually or dynamically.  More efficient and manageable.  Also more economical.

Quick app refresher.. Tailwind traders is the new contoso.  Haha.

You can scale number of instances in the Azure console, through an ARM template, or use AutoScale.
You have to know how your application behaves.  What is your baseline?
You can add multiple rules and if any rules are met then it will scale up.  If you have multiple rules for scaling down, ALL rules must be met to scale down.
How does application work with session state?  You really have to know how your application works.

What should minimum size be for number of instances?  Not 1.  As there is only single point of failure.
More than 1 has resiliency.

Autoscaling specification
Profile
Capacity (min, max, default)
Rules (Trigger, scale saction)
Recurrence

How to handle localised failure..?
-Regions
-Geographics
-Availability sets
-Availability zones

Region pairs aka.ms/region-pairs  
Horizontal architecture
Data consistency
Active/active or active/passive
Data sovereignty

Azure front door
Global HTTP load balancing with instant failover (apparently.. Instant can vary in time)
Bonus:
SSL offloading and application acceleration at the edge close to end users
Application firewall and DDoS protection
Central control plane for traffic orchestration
Actionable insights about your users and backends
Infrastructure has to be in place before you deploy front door

Virtual Machine Scale Set
Autoscaling group in AWS, the same I guess

Future directions of scaling
See slides :)  I am out of time!

### Responding to and learning from failure
Failures are going to happen because people are involve.
Share your failures and learnings.

Reacting to a problem vs
Responding to a problem  

We have to be ready

Reacting to failure means
Unplanned work
Context switching
Confusion
Increased time to repair

Mean time to recover (MTTR)
On average, how long does it take to restore service when a service incident occurs?
DORA: State of DevOps report 2016

Cost of downtime
Deployment frequency X Change failure rate X Mean time to recover X Hourly cost of outage

Not fine!  (Anti-patterns)
Alerts to inbox
Alerts to common channel
Shoulder tapping
Delays in communication
Tiered and off-shore support.  If it's not written by them they won't know why.  Engineers have to be first people to respond.
Network Operations Center (NOC)

Communication and collaboration
Create space - Alert First Responders (Software engineer on call, scheduled on call rotation, must be aware of escalation path.  Who is the next person to call?) - Alert additional stakeholders (Be overly communicative.  Be able to point and alert other people because no single person knows how the entire system works).

No first responder tools in Azure, but there are some things to help you in Azure
Azure Logic Apps SRE50-LOGIC
Microsoft Teams 
Application Insights Action Groups SRE50-AG

Severity of an incident
Detection - Response (1/3 of the entire lifecycle) - Remediation - Analysis - Readiness
How can we cut each phase in half thereby reducing the length of the incident?

ChatOps - put everything into chat
Increased collaboration
Increased sharing of domain knowledge
Increased visibility and awareness
Enhanced learning
Improved empathy
Pushing context
Read only data retrieval
Bi directional interactions
Custom infrastructure interaction

Chat bots on MS learn
aka.ms/SRE50-chatbot

Usually there is no one root cause.  What caused the problem is not linear.  How do things really work?  Including the people.  How can we make things better?

Create a welcoming judgement free space.  Everyone should feel confident and be able to ask dumb questions.

Don’t find blame, but get an account of what happened.

Countermeasures
See the slide
