MongoSessionProvider
====================

ASP.NET Session Provider for MongoDB

Installation:
Add Override Nuget feed source https://www.myget.org/F/lotosbin-public-nuget/api/v2
```
PM> Install-Package PVL.MongoSessionProvider
```

NuGet Pacakge Link: https://nuget.org/packages/PVL.MongoSessionProvider

Code: https://github.com/prasannavl/MongoSessionProvider


Example session document:

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

   

Scheduled session cleanup command:
db.Sessions.remove({"Expires" : {$lt : new Date() }})
   
Example web.config settings:

    ..
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
    .. 

# publish nuget package
```
..\.nuget\nuget pack

..\.nuget\nuget push PVL.MongoSessionProvider.2.0.0.0.nupkg -Source https://www.myget.org/F/lotosbin-public-nuget/api/v2/package

..\.nuget\nuget setapikey key -Source https://www.myget.org/F/lotosbin-public-nuget/api/v2/package 
```
