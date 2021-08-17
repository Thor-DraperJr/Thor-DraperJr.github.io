Another tech tutorial!

I've been on a productivity kick for forever. I've also been looking for an excuse to post things on Twitter. With that simple premise I thought it'd be cool if I could use some cloud tools to collect my tweets and create some dashboards telling me if I'm spending my time well or if I'm just spending my time.

## Introduction

From a high level: I'm going to use an Azure Logic App to pull my tweets and store them in a SQL database. From there I'm going to use Power BI to connect to the SQL database and transform the data into pretty visuals.

It's nothing too crazy and primarily depends on the structure of my tweets.

![1](/assets/images/1-tweet-structure.png)

The Key:
* Hashtag 1: TimeSpent OR TimeWellSpent
* Hashtag 2: The main category on what I was spending my time on (Learning, Exercise, etc.)
* Hashtag 3: The specific Activity (Azure, Peloton, etc.)

## The Order
The order that you'll need to deploy:
1. Create the SQL Database
    - Create the table and columns for the data
2. Create the Logic App
    - Connect to Twitter
    - Create a Trigger based off of a new tweet from my account
    - Create an Action to insert a new row into the SQL database
3. Connect Power BI to the SQL database
    - Transform the data
    - Create Visualizations
    - Set a schedule for the data to refresh

### step 1: create a place to store the data
Azure SQL Database is a relational database-as-a-service (DBaaS) hosted in Azure that falls into the industry category of Platform-as-a-Service (PaaS).

create a server, table, and columns for the tweet, i kept it simple and only cared about TweetData and CreatedDate

```sql
CREATE TABLE TweetData (
    CreatedAt datetime,
    TweetText varchar(512),
);
```
from the SQL server you can use the Query editor to put in the command to create your table and columns directly from the azure portal

### step 2: connect to the twitter account
Azure Logic Apps is a cloud-based platform for creating and running automated workflows that integrate your apps, data, services, and systems. Technically, a connector is a proxy or a wrapper around an API that the underlying service uses to communicate with Azure Logic Apps. When you build workflows using Azure Logic Apps, you can use connectors to help you quickly and easily access data, events, and resources in other apps, services, systems, protocols, and platforms - often without writing any code.
### step 3: set the first trigger
[When a new tweet is posted](https://docs.microsoft.com/en-us/connectors/twitter/#when-a-new-tweet-is-posted)

`from:@Thor_DraperJr, #TimeSpent OR #TimeWellSpent`
Search the text of the tweet for anything from my account that has the hashtag #TimeSpent or #TimeWellSpent
`How often do you want to check for items? 1(once ever) Hour`
set to recur once every hour
### step 4: set an action
[insert row](https://docs.microsoft.com/en-us/connectors/sql/#insert-row-(v2))

Insert row (V2)
Server name:`Use connection settings (thordraperjr-sql-server-01.database.windows.net)`
*Database name: `Use connection settings (sql-01)`
*Table name: `TweetData`
Parmeter 1: `CreatedAt` `Created at`<--Dynamic content
Parmeter 2: `TweetText` `⁠Tweet text`<--Dynamic content
⁠
### step 5: sign up for power bi
you need to have a work/organization account for the trial, download the desktop app

#### Get data
SQL Server: thordraperjr-sql-server-01.database.windows.net
Database Connectivity mode: Import (unfortunately DirectQuery isn't an option as we'll need to transform the data)

#### Transform data
APPLIED STEPS
1. Source
2. Navigation
3. Split Column by Delimeter 1 <---select a custom delimeter as a #
4. Right click column 4 <---select the delimerter `Space`

### step 6: make your visualizations
In the visualiztion tab you'll see images where you can choose a type of graph. directly underneath that you have three icons: Field, Format, Analytics. Underneath that you have the option to put in information for the graph. I made the Legend and the Values match data 

I used a Pie chart(Legend/Values = TweetText.2/Count of TweetText.2), a Funnel chart (Group/Values = TweetText.3/Count of TweetText.3), and a Donut chart (Legend/Values = TweetText.4/Count of TweetText4). Although, i'm probably changing that as more data is in the table)

Next clicking the Analytics button will let you customize the Legend, Data colors, and Title. 

### step 7: auto refresh
from the powerbi web portal you can schedule a data refress to make sure that you charts are up to date

# Create SQL Database
_Basics_
**Project details**
Subscription: Azure subscription 1
	Resource Group: rg-01
**Database details**
Database name: sql-01
Server: thordraperjr-sql-server-01
	+Username: 
	+Password: 
Want to use SQL elastic pool? No
Compute + storage: Basic
**Backup storage redundancy**
Backup storage redundancy: Locally-redundant backup storage - Preview

_Networking_
**Network connectivity**
Connectivity method: No access
**Connection Policy**
Connection policy: Default
**Encrypted connections**
Minimum TLS version: TLS 1.2

_Security_
**Azure Defender for SQL**
Enable Azure Defender for SQL: []Start free trial(30 Days)[x]Not now

_Additional settings_
**Datasource**
Use existing data: None
**Database collation**
Collation: SQL_Latin_General_CP1_CI_AS
**Maintenance window**
Maintenance window: System default (5pm to 8am)

_Tags_
Development:Twitter-to-PowerBi-App

```sql
CREATE TABLE TweetData (
    CreatedAt datetime,
    TweetText varchar(512),
);
```
^Creating a table with two columns
* `Drop TABLE TweetData;` <---Delete the entire table
* `ALTER TABLE dbo.TweetData ADD CreatedAt datetime;` <--Add a column
* `SELECT CreatedDate, TweetText FROM TweetData;` <--- Select all info in columns
* `DELETE FROM TweetData;` <--- deleting all data in the SQL database

# Logic App

from:@Thor_DraperJr, #TimeSpent OR #TimeWellSpent

# Troubleshooting
Keep in mind if you locked down your SQL server you'll need to find the range of IP address that are trying to do refreshes