MongoSessionProvider
====================

ASP.NET Session Provider for MongoDB

http://www.prasannavl.com/2013/02/mongodb-session-state-provider-for.html
MongoDB Session State Provider for ASP.NET

I've been pretty impressed with the recent development of MongoDB, and it seems to me that their one biggest problem of data consistency has now been solved. 

And so, I decided to give it base our upcoming project, Launchark (http://www.launchark.com) fully on MongoDB. But after some Googling I found out all the session providers out there are pretty outdated using deprecated libraries, or not suited for high-performance needs.

So, here's a session provider for ASP.NET.

Installation:
PM> Install-Package PVL.MongoSessionProvider 

NuGet Pacakge Link: https://nuget.org/packages/PVL.MongoSessionProvider/
Code: https://github.com/prasannavl/MongoSessionProvider


Example session document:
<code>
> use SessionState;
> db.Sessions.find().pretty();
{
        "_id" : "i2guetwsm0mgaibb1gqmodfq",
        "App" : "/",
        "Created" : ISODate("2013-02-21T22:27:32.091Z"),
        "Expires" : ISODate("2013-02-22T22:30:59.267Z"),
        "LockDate" : ISODate("2013-02-21T22:29:54.481Z"),
        "LockId" : 1,
        "Timeout" : 20,
        "Locked" : true,
        "Items" : "AQAAAP////8EVGVzdAgAAAABBkFkcmlhbg==",
        "Flags" : 0
     }
    
</code>

Scheduled session cleanup command:
db.Sessions.remove({"Expires" : {$lt : new Date() }})
    
Example web.config settings
<code>
<connectionStrings>
   <add name="SessionState" connectionString="mongodb://localhost"/>
</connectionStrings>
<system.web>
   <sessionState mode="Custom" timeout="1440" cookieless="false" customProvider="MongoSessionStateProvider">
     <providers>
       <add name="MongoSessionStateProvider" type="PVL.MongoSessionProvider" connectionStringName="SessionState" writeExceptionsToEventLog="false"/>
     </providers>
   </sessionState>
</system.web>
</code>
 Happy Coding!
