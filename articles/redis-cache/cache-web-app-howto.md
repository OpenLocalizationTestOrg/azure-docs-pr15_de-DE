<properties 
    pageTitle="So erstellen Sie eine Web App mit Cache Redis | Microsoft Azure" 
    description="Informationen Sie zum Erstellen einer Web App mit Redis Cache" 
    services="redis-cache" 
    documentationCenter="" 
    authors="steved0x" 
    manager="douge" 
    editor=""/>

<tags 
    ms.service="cache" 
    ms.workload="tbd" 
    ms.tgt_pltfrm="cache-redis" 
    ms.devlang="na" 
    ms.topic="hero-article" 
    ms.date="10/11/2016" 
    ms.author="sdanie"/>

# <a name="how-to-create-a-web-app-with-redis-cache"></a>So erstellen Sie eine Web App mit Redis Cache

> [AZURE.SELECTOR]
- [.NET](cache-dotnet-how-to-use-azure-redis-cache.md)
- [ASP.NET](cache-web-app-howto.md)
- [Node.js](cache-nodejs-get-started.md)
- [Java](cache-java-get-started.md)
- [Python](cache-python-get-started.md)

In diesem Lernprogramm erfahren zum Erstellen und Bereitstellen einer ASP.NET Web-Anwendung mit einer Web App-Verwaltungsdienst Azure Visual Studio 2015 verwenden. Die Anwendung Beispiel zeigt eine Liste der Team-Statistiken aus einer Datenbank und zeigt verschiedene Methoden zur Verwendung von Azure Redis Cache zum Speichern und Abrufen von Daten aus dem Cache. Wenn Sie das Lernprogramm abgeschlossen haben, müssen Sie die liest und schreibt in einer Datenbank, die mit Azure Redis Cache optimiert und in Azure gehostet wird eine laufenden Web app.

Lernen Sie:

-   So erstellen Sie eine Web-Anwendung ASP.NET MVC 5 in Visual Studio.
-   Wie Sie Daten aus einer Datenbank mit Entität Framework zugreifen.
-   Informationen zum Datensatz zu verbessern und reduzieren Datenbank laden, indem Sie speichern und Abrufen von Daten mithilfe von Azure Redis Cache.
-   So verwenden Sie eine Redis sortiert festlegen, um die oberen 5 Teams abzurufen.
-   Wie Sie die Azure Ressourcen für die Anwendung mithilfe einer Vorlage Ressourcenmanager bereitstellen.
-   So veröffentlichen Sie die Anwendung in Azure mit Visual Studio.

## <a name="prerequisites"></a>Erforderliche Komponenten

Wenn Sie das Lernprogramm abgeschlossen haben, müssen Sie die folgenden Vorkenntnisse verfügen.

-   [Azure-Konto](#azure-account)
-   [Visual Studio 2015 mit dem Azure SDK für .NET](#visual-studio-2015-with-the-azure-sdk-for-net)

### <a name="azure-account"></a>Azure-Konto

Sie benötigen ein Azure-Konto für dieses Lernprogramm erforderlich. Sie können:

* [Öffnen Sie ein Azure-Konto kostenlos](/pricing/free-trial/?WT.mc_id=redis_cache_hero). Sie erhalten Gutschriften, die mit dem Testen kostenpflichtiges Azure Services verwendet werden können. Auch nachdem die Gutschriften von verwendet werden, können Sie das Konto beibehalten und kostenlosen Azure Dienste und Features verwenden.
* [Vorteile für Abonnenten Visual Studio aktivieren](/pricing/member-offers/msdn-benefits-details/?WT.mc_id=redis_cache_hero). Ihr Abonnement MSDN bietet Ihnen Gutschriften jeden Monat, die Sie für kostenpflichtiges Azure-Dienste verwenden können.

### <a name="visual-studio-2015-with-the-azure-sdk-for-net"></a>Visual Studio 2015 mit dem Azure SDK für .NET

Das Lernprogramm ist für Visual Studio 2015 mit [Azure SDK für .NET](../dotnet-sdk.md) 2.8.2 geschrieben oder höher. [Das aktuelle Azure SDK für Visual Studio 2015 hier herunterladen](http://go.microsoft.com/fwlink/?linkid=518003). Visual Studio wird automatisch mit dem SDK installiert, wenn Sie noch nicht vorhanden ist.

Wenn Sie Visual Studio 2013 verfügen, können Sie [die neuesten Azure SDK für Visual Studio 2013 herunterladen](http://go.microsoft.com/fwlink/?LinkID=324322). Einige Bildschirme werden aus der Illustrationen in diesem Lernprogramm dargestellt anders angezeigt.

>[AZURE.NOTE] Je nachdem, wie viele der SDK Abhängigkeiten Sie bereits auf Ihrem Computer haben könnte Installieren des SDK langem aus eine halbe Stunde oder mehrere mehrere Minuten dauern.

## <a name="create-the-visual-studio-project"></a>Erstellen des Visual Studio-Projekts

1. Öffnen Sie Visual Studio, und klicken Sie auf **Datei**, **neu**, **Projekt**.

2. Erweitern Sie den **Visual C#-** Knoten in der Liste **Vorlagen** , wählen Sie die **Cloud**und klicken Sie auf **ASP.NET Web-Anwendung**. Stellen Sie sicher, dass **.NET Framework 4.5.2** ausgewählt ist.  Geben Sie in das Textfeld **Name** **ContosoTeamStats** ein, und klicken Sie auf **OK**.
 
    ![Erstellen von project][cache-create-project]

3. Wählen Sie als Projekttyp **MVC** aus. Deaktivieren Sie das Kontrollkästchen **Host in der Cloud** . Sie erhalten im Lernprogramm [Azure Bereitstellungsressourcen](#provision-the-azure-resources) und [Veröffentlichen Sie die Anwendung in Azure](#publish-the-application-to-azure) in nachfolgenden Schritten. Ein Beispiel für die Bereitstellung von einer App-Dienst Web app Visual Studio durch verlassen **Host in der Cloud** aktiviert finden Sie unter [Erste Schritte mit Web Apps in Azure-App-Verwaltungsdienst, mit ASP.NET und Visual Studio](../app-service-web/web-sites-dotnet-get-started.md).

    ![Wählen Sie die Projektvorlage][cache-select-template]

4. Klicken Sie auf **OK** , um das Projekt zu erstellen.

## <a name="create-the-aspnet-mvc-application"></a>Erstellen der ASP.NET-MVC-Anwendung

In diesem Abschnitt des Lernprogramms erstellen Sie die grundlegende Anwendung, die liest und Team-Statistiken aus einer Datenbank angezeigt.

-   [Fügen Sie das Modell hinzu.](#add-the-model)
-   [Fügen Sie dem Controller hinzu.](#add-the-controller)
-   [Konfigurieren von Ansichten](#configure-the-views)

### <a name="add-the-model"></a>Fügen Sie das Modell hinzu.

1. Mit der rechten Maustaste **Modelle** in **Lösung-Explorer**, und wählen Sie **Hinzufügen**, **Class**. 

    ![Hinzufügen von Modell][cache-model-add-class]

2. Geben Sie `Team` für die Klasse einen Namen ein, und klicken Sie auf **Hinzufügen**.

    ![Fügen Sie Modellklasse][cache-model-add-class-dialog]

3. Ersetzen der `using` Anweisungen am oberen Rand der `Team.cs` Datei mit folgenden Anweisungen verwenden.


        using System;
        using System.Collections.Generic;
        using System.Data.Entity;
        using System.Data.Entity.SqlServer;


4. Ersetzen Sie die Definition von der `Team` Klasse mit den folgenden Codeausschnitt, die eine aktualisierte enthält `Team` Klasse Definition sowie einige andere Entität Framework Helper Klassen. Weitere Informationen zu der Code für die erste Ansatz zum Entität Framework, das in diesem Lernprogramm verwendet wird, finden Sie unter [Code zuerst in eine neue Datenbank](https://msdn.microsoft.com/data/jj193542).


        public class Team
        {
            public int ID { get; set; }
            public string Name { get; set; }
            public int Wins { get; set; }
            public int Losses { get; set; }
            public int Ties { get; set; }
        
            static public void PlayGames(IEnumerable<Team> teams)
            {
                // Simple random generation of statistics.
                Random r = new Random();
        
                foreach (var t in teams)
                {
                    t.Wins = r.Next(33);
                    t.Losses = r.Next(33);
                    t.Ties = r.Next(0, 5);
                }
            }
        }
        
        public class TeamContext : DbContext
        {
            public TeamContext()
                : base("TeamContext")
            {
            }
        
            public DbSet<Team> Teams { get; set; }
        }
        
        public class TeamInitializer : CreateDatabaseIfNotExists<TeamContext>
        {
            protected override void Seed(TeamContext context)
            {
                var teams = new List<Team>
                {
                    new Team{Name="Adventure Works Cycles"},
                    new Team{Name="Alpine Ski House"},
                    new Team{Name="Blue Yonder Airlines"},
                    new Team{Name="Coho Vineyard"},
                    new Team{Name="Contoso, Ltd."},
                    new Team{Name="Fabrikam, Inc."},
                    new Team{Name="Lucerne Publishing"},
                    new Team{Name="Northwind Traders"},
                    new Team{Name="Consolidated Messenger"},
                    new Team{Name="Fourth Coffee"},
                    new Team{Name="Graphic Design Institute"},
                    new Team{Name="Nod Publishers"}
                };
        
                Team.PlayGames(teams);
        
                teams.ForEach(t => context.Teams.Add(t));
                context.SaveChanges();
            }
        }
        
        public class TeamConfiguration : DbConfiguration
        {
            public TeamConfiguration()
            {
                SetExecutionStrategy("System.Data.SqlClient", () => new SqlAzureExecutionStrategy());
            }
        }


2. Doppelklicken Sie auf **Lösung Explorer** **web.config** , um ihn zu öffnen.

    ![Web.config][cache-web-config]

3.  Fügen Sie die folgende Verbindungszeichenfolge verweist auf die `connectionStrings` Abschnitt. Der Name der Verbindungszeichenfolge muss den Namen der Entität Framework Datenbank Kontext-Klasse also übereinstimmen `TeamContext`.

        <add name="TeamContext" connectionString="Data Source=(LocalDB)\v11.0;AttachDbFilename=|DataDirectory|\Teams.mdf;Integrated Security=True" providerName="System.Data.SqlClient" />


    Nach dem Hinzufügen, die `connectionStrings` Abschnitt sollte wie im folgenden Beispiel aussehen.


        <connectionStrings>
            <add name="DefaultConnection" connectionString="Data Source=(LocalDb)\MSSQLLocalDB;AttachDbFilename=|DataDirectory|\aspnet-ContosoTeamStats-20160216120918.mdf;Initial Catalog=aspnet-ContosoTeamStats-20160216120918;Integrated Security=True"
                providerName="System.Data.SqlClient" />
            <add name="TeamContext" connectionString="Data Source=(LocalDB)\v11.0;AttachDbFilename=|DataDirectory|\Teams.mdf;Integrated Security=True"  providerName="System.Data.SqlClient" />
        </connectionStrings>

### <a name="add-the-controller"></a>Fügen Sie dem Controller hinzu.

1. Drücken Sie **F6** , um das Projekt erstellen. 
2. Klicken Sie im **Explorer Lösung**mit der rechten Maustaste in des Ordners **Controller** , und wählen Sie **Hinzufügen**, **Controller**.

    ![Controller hinzufügen][cache-add-controller]

3. Wählen Sie **MVC 5 Controller mit Ansichten, die mithilfe von Entität Framework**aus, und klicken Sie auf **Hinzufügen**. Wenn Sie eine Fehlermeldung erhalten, nachdem Sie auf **Hinzufügen**, stellen Sie sicher, dass Sie zuerst das Projekt erstellt haben.

    ![Hinzufügen von Controller-Klasse][cache-add-controller-class]

5. Wählen Sie aus der Dropdownliste **Modellklasse** **Team (ContosoTeamStats.Models)** aus. Wählen Sie aus der Dropdownliste **Daten Kontext Class** **TeamContext (ContosoTeamStats.Models)** aus. Typ `TeamsController` im Textfeld Name **Controller** (wenn es nicht automatisch ausgefüllt wird). Klicken Sie auf **Hinzufügen** , um die Controller-Klasse erstellen und die Standardansichten hinzufügen.

    ![Konfigurieren von controller][cache-configure-controller]

4. Klicken Sie im **Explorer Lösung**erweitern Sie **Global.asax** , und doppelklicken Sie auf **Global.asax.cs** , um ihn zu öffnen.

    ![Global.asax.cs][cache-global-asax]

5. Fügen Sie die folgenden beiden mit Anweisungen am oberen Rand der Datei unter anderen Anweisungen verwenden.


        using System.Data.Entity;
        using ContosoTeamStats.Models;


6. Fügen Sie die folgende Zeile des Codes am Ende der `Application_Start` Methode.


        Database.SetInitializer<TeamContext>(new TeamInitializer());


7. Erweitern Sie im **Explorer Lösung**, `App_Start` , und doppelklicken Sie auf `RouteConfig.cs`.

    ![RouteConfig.cs][cache-RouteConfig-cs]

8. Ersetzen Sie `controller = "Home"` in den folgenden Code in die `RegisterRoutes` Methode mit `controller = "Teams"` wie im folgenden Beispiel dargestellt.


        routes.MapRoute(
            name: "Default",
            url: "{controller}/{action}/{id}",
            defaults: new { controller = "Teams", action = "Index", id = UrlParameter.Optional }
        );


### <a name="configure-the-views"></a>Konfigurieren von Ansichten

1. Im **Explorer Lösung**erweitern Sie den Ordner " **Ansichten** " und dann auf den **freigegebenen** Ordner, und doppelklicken Sie auf **_Layout.cshtml**. 

    ![_Layout.cshtml][cache-layout-cshtml]

2. Ändern des Inhalts der `title` Element, und Ersetzen `My ASP.NET Application` mit `Contoso Team Stats` wie im folgenden Beispiel dargestellt.


        <title>@ViewBag.Title - Contoso Team Stats</title>


3. In der `body` Abschnitt, aktualisieren Sie die erste `Html.ActionLink` Anweisung und Ersetzen `Application name` mit `Contoso Team Stats` , und Ersetzen Sie `Home` mit `Teams`.
    -   Vorher:`@Html.ActionLink("Application name", "Index", "Home", new { area = "" }, new { @class = "navbar-brand" })`
    -   Nach:`@Html.ActionLink("Contoso Team Stats", "Index", "Teams", new { area = "" }, new { @class = "navbar-brand" })`

    ![Ändern von Code][cache-layout-cshtml-code]

4. Drücken Sie **STRG + F5,** um zu erstellen, und führen Sie die Anwendung. Diese Version der Anwendung liest die Ergebnisse direkt aus der Datenbank. Beachten Sie die **Neu erstellen**, **Bearbeiten**, **Details**und **Löschen von** Aktionen, die mit der Anwendung durch die Scaffold **MVC 5 Controller mit Ansichten, die mithilfe von Entität Framework** automatisch hinzugefügt wurden. Im nächsten Abschnitt des Lernprogramms fügen Sie Redis Cache zur Optimierung der Datenzugriff und bieten zusätzliche Features für die Anwendung.

![Starter-Anwendung][cache-starter-application]

## <a name="configure-the-application-to-use-redis-cache"></a>Konfigurieren Sie die Anwendung Redis Cache verwenden

In diesem Abschnitt des Lernprogramms werden Sie die Anwendung Beispiel zum Speichern und Abrufen von Contoso-Team-Statistiken aus einer Instanz Azure Redis Cache mithilfe des [StackExchange.Redis](https://github.com/StackExchange/StackExchange.Redis) -Cache-Clients konfigurieren.

-   [Konfigurieren Sie die Anwendung StackExchange.Redis verwenden](#configure-the-application-to-use-stackexchangeredis)
-   [Aktualisieren Sie die TeamsController-Klasse, um die Ergebnisse aus dem Cache oder Datenbank zurück](#update-the-teamscontroller-class-to-return-results-from-the-cache-or-the-database)
-   [Aktualisieren der erstellen, bearbeiten und löschen Methoden für die Arbeit mit den cache](#update-the-create-edit-and-delete-methods-to-work-with-the-cache)
-   [Aktualisieren Sie die Ansicht Teams Index für die Arbeit mit den cache](#update-the-teams-index-view-to-work-with-the-cache)


### <a name="configure-the-application-to-use-stackexchangeredis"></a>Konfigurieren Sie die Anwendung StackExchange.Redis verwenden

1. Um eine Clientanwendung in Visual Studio mit dem StackExchange.Redis NuGet Package konfigurieren, mit der rechten Maustaste im Projekts im **Solution Explorer** , und wählen Sie **NuGet Pakete verwalten**. 

    ![NuGet-Pakete verwalten][redis-cache-manage-nuget-menu]

2. Geben Sie **StackExchange.Redis** in das Suchtextfeld ein, wählen Sie die gewünschte Version aus den Ergebnissen aus, und klicken Sie auf **Installieren**.

    ![StackExchange.Redis NuGet-Paket][redis-cache-stack-exchange-nuget]

    Das Paket NuGet downloads und fügt die erforderlichen Assemblyverweise für Ihre Clientanwendung auf Azure Redis Cache mit dem StackExchange.Redis Cacheclient zugreifen. Wenn Sie eine Version starken Namen der Clientbibliothek **StackExchange.Redis** verwenden möchten, wählen Sie **StackExchange.Redis.StrongName**; Wählen Sie andernfalls **StackExchange.Redis**aus.

3. Klicken Sie im **Explorer Lösung**erweitern Sie den Ordner **Controller** , und doppelklicken Sie auf **TeamsController.cs** , um ihn zu öffnen.

    ![Teams controller][cache-teamscontroller]

4. Fügen Sie die folgenden beiden **TeamsController.cs**-Anweisungen verwenden.

        using System.Configuration;
        using StackExchange.Redis;

5. Die folgenden zwei Eigenschaften zum Hinzufügen der `TeamsController` Class.

        // Redis Connection string info
        private static Lazy<ConnectionMultiplexer> lazyConnection = new Lazy<ConnectionMultiplexer>(() =>
        {
            string cacheConnection = ConfigurationManager.AppSettings["CacheConnection"].ToString();
            return ConnectionMultiplexer.Connect(cacheConnection);
        });
    
        public static ConnectionMultiplexer Connection
        {
            get
            {
                return lazyConnection.Value;
            }
        }
  
1. Erstellen Sie eine Datei auf Ihrem Computer mit dem Namen `WebAppPlusCacheAppSecrets.config` , und setzen Sie es an einem Speicherort, die mit den Quellcode Ihrer Anwendung Stichprobe wird nicht geprüft werden sollten Sie entscheiden, um es in ein anderes zu prüfen. In diesem Beispiel die `AppSettingsSecrets.config` Datei befindet sich unter `C:\AppSecrets\WebAppPlusCacheAppSecrets.config`.

    Bearbeiten der `WebAppPlusCacheAppSecrets.config` Datei, und fügen Sie den folgenden Inhalt hinzu. Wenn Sie die Anwendung lokal ausgeführt wird diese Informationen für die Verbindung zu Ihrer Redis Azure-Cache-Instanz verwendet. Später im Lernprogramm Sie bereitstellen eine Instanz Azure Redis Cache und aktualisieren den Cache Namen und das Kennwort. Wenn Sie nicht die Stichprobe-Anwendung lokal ausführen möchten können Sie die Erstellung von dieser Datei und die nachfolgenden Schritte, in denen die Datei verwiesen überspringen, da beim Bereitstellen für Azure die Anwendung die Verbindungsinformationen Cache aus der app-Einstellung für das Web App und nicht aus dieser Datei abruft. Da der `WebAppPlusCacheAppSecrets.config` bereitgestellt wird nicht in Azure mit Ihrer Anwendung, ist dies nicht erforderlich, wenn Sie beabsichtigen, die Anwendung lokal ausführen.


        <appSettings>
          <add key="CacheConnection" value="MyCache.redis.cache.windows.net,abortConnect=false,ssl=true,password=..."/>
        </appSettings>


2. Doppelklicken Sie auf **Lösung Explorer** **web.config** , um ihn zu öffnen.

    ![Web.config][cache-web-config]

3. Fügen Sie den folgenden `file` Attribut, um die `appSettings` Element. Wenn Sie einen anderen Namen oder Speicherort verwendet haben, ersetzen Sie diese Werte für die Regeln, die im Beispiel dargestellt.
    -   Vorher:`<appSettings>`
    -   Nach:` <appSettings file="C:\AppSecrets\WebAppPlusCacheAppSecrets.config">`

    Die Laufzeit ASP.NET führt den Inhalt der externen Datei durch das Markup in der `<appSettings>` Element. Die Laufzeit ignoriert das Dateiattribut aus, wenn die angegebene Datei nicht gefunden werden kann. Ihre vertraulichen Daten (die Verbindungszeichenfolge in Ihren Cache) sind nicht als Teil des Quellcodes für die Anwendung enthalten. Wenn Sie die Web app Azure bereitstellen der `WebAppPlusCacheAppSecrests.config` Datei wird nicht bereitgestellt (das ist, was Sie möchten). Es gibt mehrere Methoden zum geheimen Schlüssel in Azure angeben und in diesem Lernprogramm sie sind konfiguriert automatisch für Sie, wenn Sie in einem weiteren Lernprogramm [Azure Bereitstellungsressourcen](#provision-the-azure-resources) Schritt. Weitere Informationen zum Arbeiten mit vertrauliche Informationen in Azure finden Sie unter [bewährte Methoden zum Bereitstellen von Kennwörtern und andere vertraulichen Daten zu ASP.NET und Azure-App-Dienst](http://www.asp.net/identity/overview/features-api/best-practices-for-deploying-passwords-and-other-sensitive-data-to-aspnet-and-azure).


### <a name="update-the-teamscontroller-class-to-return-results-from-the-cache-or-the-database"></a>Aktualisieren Sie die TeamsController-Klasse, um die Ergebnisse aus dem Cache oder Datenbank zurück

In diesem Beispiel können Team Statistiken aus der Datenbank oder aus dem Cache abgerufen werden. Team-Statistiken werden im Cache als ein serialisiertes gespeichert `List<Team>`, und auch als sortierten Satz Redis Datentypen verwenden. Wenn Sie Elemente aus einem sortierten Satz abrufen, können Sie alle einige, abrufen, oder Abfragen für bestimmte Elemente. In diesem Beispiel wird den sortierten Satz für die obersten 5 Teams Anzahl Wins Rangfolge abgefragt werden.

>[AZURE.NOTE] Es ist nicht erforderlich, um die Team-Statistiken in mehreren Formaten im Cache zu speichern, damit Azure Redis Cache verwenden können. In diesem Lernprogramm wird mit mehreren Formaten veranschaulicht einige der anderen Methoden und verschiedene Datentypen, die Sie zum Zwischenspeichern von Daten verwenden können.



1. Fügen Sie den folgenden Anweisungen, die mit den `TeamsController.cs` Datei oben mit anderen Anweisungen verwenden.

        using System.Diagnostics;
        using Newtonsoft.Json;

2. Ersetzen Sie das aktuelle `public ActionResult Index()` Methode mit der folgenden Implementierung.


        // GET: Teams
        public ActionResult Index(string actionType, string resultType)
        {
            List<Team> teams = null;
        
            switch(actionType)
            {
                case "playGames": // Play a new season of games.
                    PlayGames();
                    break;
        
                case "clearCache": // Clear the results from the cache.
                    ClearCachedTeams();
                    break;
        
                case "rebuildDB": // Rebuild the database with sample data.
                    RebuildDB();
                    break;
            }
        
            // Measure the time it takes to retrieve the results.
            Stopwatch sw = Stopwatch.StartNew();
        
            switch(resultType)
            {
                case "teamsSortedSet": // Retrieve teams from sorted set.
                    teams = GetFromSortedSet();
                    break;
        
                case "teamsSortedSetTop5": // Retrieve the top 5 teams from the sorted set.
                    teams = GetFromSortedSetTop5();
                    break;
        
                case "teamsList": // Retrieve teams from the cached List<Team>.
                    teams = GetFromList();
                    break;
        
                case "fromDB": // Retrieve results from the database.
                default:
                    teams = GetFromDB();
                    break;
            }
        
            sw.Stop();
            double ms = sw.ElapsedTicks / (Stopwatch.Frequency / (1000.0));

            // Add the elapsed time of the operation to the ViewBag.msg.
            ViewBag.msg += " MS: " + ms.ToString();
        
            return View(teams);
        }


3. Die folgenden drei Methoden zum Hinzufügen der `TeamsController` Klasse zum Implementieren der `playGames`, `clearCache`, und `rebuildDB` Aktionstypen aus der Switch-Anweisung, die im vorherigen Codeausschnitt hinzugefügt.

    Die `PlayGames` Methode aktualisiert die Team-Statistiken durch Simulieren einer Jahreszeit Spiele speichert die Ergebnisse in der Datenbank und löscht die jetzt veralteten Daten aus dem Cache.


        void PlayGames()
        {
            ViewBag.msg += "Updating team statistics. ";
            // Play a "season" of games.
            var teams = from t in db.Teams
                        select t;
    
            Team.PlayGames(teams);
    
            db.SaveChanges();
    
            // Clear any cached results
            ClearCachedTeams();
        }


    Die `RebuildDB` Methode die Datenbank mit dem Standardsatz von Teams reinitialisiert Statistiken für diese generiert und löscht die jetzt veralteten Daten aus dem Cache.
    
        void RebuildDB()
        {
            ViewBag.msg += "Rebuilding DB. ";
            // Delete and re-initialize the database with sample data.
            db.Database.Delete();
            db.Database.Initialize(true);

            // Clear any cached results
            ClearCachedTeams();
        }


    Die `ClearCachedTeams` Methode entfernt alle zwischengespeicherten Team-Statistiken aus dem Cache.

    
        void ClearCachedTeams()
        {
            IDatabase cache = Connection.GetDatabase();
            cache.KeyDelete("teamsList");
            cache.KeyDelete("teamsSortedSet");
            ViewBag.msg += "Team data removed from cache. ";
        } 


4. Fügen Sie die folgenden vier Methoden, um die `TeamsController` Klasse, um die verschiedenen Optionen zum Abrufen von der Teamwebsite Statistik aus dem Cache und die Datenbank zu implementieren. Jede dieser Methoden gibt eine `List<Team>` die dann von der Ansicht angezeigt wird.

    Die `GetFromDB` Methode liest die Team-Statistiken aus der Datenbank.

        List<Team> GetFromDB()
        {
            ViewBag.msg += "Results read from DB. ";
            var results = from t in db.Teams
                orderby t.Wins descending
                select t; 
    
            return results.ToList<Team>();
        }


    Die `GetFromList` Methode liest die Team-Statistiken aus dem Cache als ein serialisiertes `List<Team>`. Ist eine Cache verpassen, sind die Team-Statistiken aus der Datenbank gelesen und klicken Sie dann im Cache für eine erneute Verwendung gespeichert. In diesem Beispiel verwenden wir JSON.NET Serialisierung serialisiert .NET Objekte zu und aus dem Cache. Weitere Informationen finden Sie unter [Arbeiten mit .NET Objekte in Azure Redis Cache](cache-dotnet-how-to-use-azure-redis-cache.md#work-with-net-objects-in-the-cache).

        List<Team> GetFromList()
        {
            List<Team> teams = null;

            IDatabase cache = Connection.GetDatabase();
            string serializedTeams = cache.StringGet("teamsList");
            if (!String.IsNullOrEmpty(serializedTeams))
            {
                teams = JsonConvert.DeserializeObject<List<Team>>(serializedTeams);

                ViewBag.msg += "List read from cache. ";
            }
            else
            {
                ViewBag.msg += "Teams list cache miss. ";
                // Get from database and store in cache
                teams = GetFromDB();

                ViewBag.msg += "Storing results to cache. ";
                cache.StringSet("teamsList", JsonConvert.SerializeObject(teams));
            }
            return teams;
        }


    Die `GetFromSortedSet` Methode liest die Team-Statistiken aus einem Cache sortierten Satz. Ist eine Cache verpassen, sind die Team-Statistiken aus der Datenbank gelesen und im Cache als sortierten Satz gespeichert.


        List<Team> GetFromSortedSet()
        {
            List<Team> teams = null;
            IDatabase cache = Connection.GetDatabase();
            // If the key teamsSortedSet is not present, this method returns a 0 length collection.
            var teamsSortedSet = cache.SortedSetRangeByRankWithScores("teamsSortedSet", order: Order.Descending);
            if (teamsSortedSet.Count() > 0)
            {
                ViewBag.msg += "Reading sorted set from cache. ";
                teams = new List<Team>();
                foreach (var t in teamsSortedSet)
                {
                    Team tt = JsonConvert.DeserializeObject<Team>(t.Element);
                    teams.Add(tt);
                }
            }
            else
            {
                ViewBag.msg += "Teams sorted set cache miss. ";
    
                // Read from DB
                teams = GetFromDB();
    
                ViewBag.msg += "Storing results to cache. ";
                foreach (var t in teams)
                {
                    Console.WriteLine("Adding to sorted set: {0} - {1}", t.Name, t.Wins);
                    cache.SortedSetAdd("teamsSortedSet", JsonConvert.SerializeObject(t), t.Wins);
                }
            }
            return teams;
        }


    Die `GetFromSortedSetTop5` Methode liest die oberen 5 Teams aus dem Cache sortierten Satz. Es startet, indem Sie den Cache für das Vorhandensein der `teamsSortedSet` Schlüssel. Wenn dieser Schlüssel nicht vorhanden ist, ist die `GetFromSortedSet` wird aufgerufen, um die Team-Statistiken lesen und im Cache zu speichern. Als Nächstes wird der Cache sortierte Satz für die obersten 5 Teams abgefragt die zurückgegeben werden.


        List<Team> GetFromSortedSetTop5()
        {
            List<Team> teams = null;
            IDatabase cache = Connection.GetDatabase();

            // If the key teamsSortedSet is not present, this method returns a 0 length collection.
            var teamsSortedSet = cache.SortedSetRangeByRankWithScores("teamsSortedSet", stop: 4, order: Order.Descending);
            if(teamsSortedSet.Count() == 0)
            {
                // Load the entire sorted set into the cache.
                GetFromSortedSet();

                // Retrieve the top 5 teams.
                teamsSortedSet = cache.SortedSetRangeByRankWithScores("teamsSortedSet", stop: 4, order: Order.Descending);
            }

            ViewBag.msg += "Retrieving top 5 teams from cache. ";
            // Get the top 5 teams from the sorted set
            teams = new List<Team>();
            foreach (var team in teamsSortedSet)
            {
                teams.Add(JsonConvert.DeserializeObject<Team>(team.Element));
            }
            return teams;
        }


### <a name="update-the-create-edit-and-delete-methods-to-work-with-the-cache"></a>Aktualisieren der erstellen, bearbeiten und löschen Methoden für die Arbeit mit den cache

Der Gerüstbau Code, der als Teil der in diesem Beispiel enthält die Methoden zum Hinzufügen, bearbeiten und Löschen von Teams. Jedes Mal, wenn ein Team hinzugefügt, bearbeitet oder entfernt wird, werden die Daten im Cache veraltet. In diesem Abschnitt werden Sie diese drei Methoden, um den Cache Teams bereinigen, sodass der Cache nicht synchron mit der Datenbank kann nicht ändern.

1. Navigieren Sie zu der `Create(Team team)` Methode in der `TeamsController` Class. Hinzufügen ein Anrufs an die `ClearCachedTeams` Methode, wie im folgenden Beispiel dargestellt.


        // POST: Teams/Create
        // To protect from overposting attacks, please enable the specific properties you want to bind to, for 
        // more details see http://go.microsoft.com/fwlink/?LinkId=317598.
        [HttpPost]
        [ValidateAntiForgeryToken]
        public ActionResult Create([Bind(Include = "ID,Name,Wins,Losses,Ties")] Team team)
        {
            if (ModelState.IsValid)
            {
                db.Teams.Add(team);
                db.SaveChanges();
                // When a team is added, the cache is out of date.
                // Clear the cached teams.
                ClearCachedTeams();
                return RedirectToAction("Index");
            }
    
            return View(team);
        }


2. Navigieren Sie zu der `Edit(Team team)` Methode in der `TeamsController` Class. Hinzufügen ein Anrufs an die `ClearCachedTeams` Methode, wie im folgenden Beispiel dargestellt.


        // POST: Teams/Edit/5
        // To protect from overposting attacks, please enable the specific properties you want to bind to, for 
        // more details see http://go.microsoft.com/fwlink/?LinkId=317598.
        [HttpPost]
        [ValidateAntiForgeryToken]
        public ActionResult Edit([Bind(Include = "ID,Name,Wins,Losses,Ties")] Team team)
        {
            if (ModelState.IsValid)
            {
                db.Entry(team).State = EntityState.Modified;
                db.SaveChanges();
                // When a team is edited, the cache is out of date.
                // Clear the cached teams.
                ClearCachedTeams();
                return RedirectToAction("Index");
            }
            return View(team);
        }


3. Navigieren Sie zu der `DeleteConfirmed(int id)` Methode in der `TeamsController` Class. Hinzufügen ein Anrufs an die `ClearCachedTeams` Methode, wie im folgenden Beispiel dargestellt.


        // POST: Teams/Delete/5
        [HttpPost, ActionName("Delete")]
        [ValidateAntiForgeryToken]
        public ActionResult DeleteConfirmed(int id)
        {
            Team team = db.Teams.Find(id);
            db.Teams.Remove(team);
            db.SaveChanges();
            // When a team is deleted, the cache is out of date.
            // Clear the cached teams.
            ClearCachedTeams();
            return RedirectToAction("Index");
        }


### <a name="update-the-teams-index-view-to-work-with-the-cache"></a>Aktualisieren Sie die Ansicht Teams Index für die Arbeit mit den cache

1. Im **Explorer Lösung**erweitern Sie den Ordner **Ansichten** , klicken Sie dann den Ordner **Teams** , und doppelklicken Sie auf **Index.cshtml**.

    ![Index.cshtml][cache-views-teams-index-cshtml]

2. Suchen Sie im oberen Bereich der Datei für die folgenden Absatzelement.

    ![Aktion-Tabelle][cache-teams-index-table]

    Dies ist der Link zu einer neuen Teamwebsite erstellen. Ersetzen Sie das Absatzelement mit der folgenden Tabelle aus. Diese Tabelle hat Aktionslinks für ein neues Team erstellen, Wiedergabe einer neuen Jahreszeit Spiele, Löschen des Caches, die Teams aus dem Cache in mehreren Formaten abrufen, Abrufen der Teams aus der Datenbank, und Neuerstellen der Datenbank frisch Beispieldaten.


        <table class="table">
            <tr>
                <td>
                    @Html.ActionLink("Create New", "Create")
                </td>
                <td>
                    @Html.ActionLink("Play Season", "Index", new { actionType = "playGames" })
                </td>
                <td>
                    @Html.ActionLink("Clear Cache", "Index", new { actionType = "clearCache" })
                </td>
                <td>
                    @Html.ActionLink("List from Cache", "Index", new { resultType = "teamsList" })
                </td>
                <td>
                    @Html.ActionLink("Sorted Set from Cache", "Index", new { resultType = "teamsSortedSet" })
                </td>
                <td>
                    @Html.ActionLink("Top 5 Teams from Cache", "Index", new { resultType = "teamsSortedSetTop5" })
                </td>
                <td>
                    @Html.ActionLink("Load from DB", "Index", new { resultType = "fromDB" })
                </td>
                <td>
                    @Html.ActionLink("Rebuild DB", "Index", new { actionType = "rebuildDB" })
                </td>
            </tr>    
        </table>


3. Führen Sie einen Bildlauf an das Ende der **Index.cshtml** -Datei, und fügen Sie den folgenden `tr` Element, sodass die It der letzten Zeile in der letzten Tabelle in der Datei ist.

        <tr><td colspan="5">@ViewBag.Msg</td></tr>

    Diese Zeile zeigt den Wert der `ViewBag.Msg` der enthält eines Statusberichts zu den aktuellen Vorgang, der beim Klicken auf einen der Aktionslinks aus dem vorherigen Schritt festgelegt ist.   

    ![Meldung zum Verbindungsstatus][cache-status-message]

4. Drücken Sie **F6** , um das Projekt erstellen.

## <a name="provision-the-azure-resources"></a>Azure Bereitstellungsressourcen

Um Ihrer Anwendung in Azure zu hosten, müssen Sie zuerst die Azure Dienste bereitstellen, die die Anwendung erforderlich ist. Die Anwendung Beispiel in diesem Lernprogramm verwendet die folgenden Azure-Dienste.

-   Azure Redis Cache
-   App-Dienst Web App
-   SQL-Datenbank

Um diese Dienste zu einer neuen oder vorhandenen Ressourcengruppe Ihrer Wahl bereitstellen möchten, klicken Sie auf die folgenden **bereitstellen zu Azure** -Schaltfläche.

[! [Bereitstellen Sie für Azure] [Deploybutton]](https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fraw.githubusercontent.com%2FAzure%2Fazure-quickstart-templates%2Fmaster%2F201-web-app-redis-cache-sql-database%2Fazuredeploy.json)

Diese Schaltfläche **Bereitstellen in Azure** verwendet die [Erstellen einer Web App plus Redis Cache plus SQL-Datenbank](https://github.com/Azure/azure-quickstart-templates/tree/master/201-web-app-redis-cache-sql-database) [Azure Schnellstart](https://github.com/Azure/azure-quickstart-templates) -Vorlage zum Bereitstellen dieser Dienste und Festlegen der Verbindungszeichenfolge für die SQL-Datenbank und die anwendungseinstellung für die Verbindungszeichenfolge Azure Redis Cache.

>[AZURE.NOTE] Wenn Sie ein Azure-Konto besitzen, können Sie den [ein kostenloses Azure-Konto erstellen](https://azure.microsoft.com/pricing/free-trial/?WT.mc_id=redis_cache_hero) , in dem nur ein paar Minuten.

Durch Klicken auf die Schaltfläche **bereitstellen zu Azure** gelangen Sie Azure-Portal an und leitet den Vorgang des Erstellens von der Ressourcen, die durch die Vorlage beschrieben.

![Bereitstellen für Azure][cache-deploy-to-azure-step-1]

1. Klicken Sie auf das **benutzerdefinierte Bereitstellung** Blade wählen Sie aus dem Azure Abonnement verwenden möchten, und wählen Sie eine vorhandene Ressourcengruppe oder einen neuen erstellen, und geben Sie den Speicherort der Ressource Gruppe.
2. Geben Sie auf das Blade **Parameter** einen Administratorkontonamen (**ADMINISTRATORLOGIN** - **Administrator**nicht verwenden), Login Administratorkennwort (**ADMINISTRATORLOGINPASSWORD**) und Datenbankname (**Datenbankname**). Die anderen Parameter sind für eine kostenlose App-Verwaltungsdienst Hostinganbieter Plan und niedrigere Kosten Optionen für SQL-Datenbank und Azure Redis Cache, die im Zusammenhang mit einer kostenlosen Ebene nicht konfiguriert.
3. Ändern Sie die anderen Einstellungen bei Bedarf, oder übernehmen Sie die Standardeinstellungen, und klicken Sie auf **OK**.


![Bereitstellen für Azure][cache-deploy-to-azure-step-2]

1. Klicken Sie auf **Überprüfen Vertragsbedingungen**.
2. Lesen Sie die Konditionen auf das Blade **kaufen** , und klicken Sie auf **kaufen**.
3. Um zu beginnen, die Ressourcen bereitgestellt, klicken Sie auf das **benutzerdefinierte Bereitstellung** Blade auf **Erstellen** .

Um den Fortschritt der Bereitstellung anzeigen möchten, klicken Sie auf das Benachrichtigungssymbol, und klicken Sie auf **Bereitstellung gestartet**.

![Bereitstellung gestartet][cache-deployment-started]

Sie können den Status der Bereitstellung auf das Blade **Microsoft.Template** anzeigen.

![Bereitstellen für Azure][cache-deploy-to-azure-step-3]

Wenn provisioning abgeschlossen ist, können Sie Ihrer Anwendung und Azure aus Visual Studio veröffentlichen.

>[AZURE.NOTE] Fehlern, die bei der Bereitstellung auftreten können, werden auf das Blade **Microsoft.Template** angezeigt. Häufige Fehler sind zu viele SQL Server oder zu viele kostenlosen App-Verwaltungsdienst Hostinganbieter Pläne pro Abonnement. Beheben von Fehlern und den Prozess, indem Sie **erneut** auf das Blade **Microsoft.Template** oder die Schaltfläche **bereitstellen zu Azure** in diesem Lernprogramm.

## <a name="publish-the-application-to-azure"></a>Veröffentlichen Sie die Anwendung in Azure

In diesem Schritt des Lernprogramms werden Sie veröffentlichen Sie die Anwendung in Azure, und führen Sie es in der Cloud.

1. Mit der rechten Maustaste in des Projekts **ContosoTeamStats** in Visual Studio, und wählen Sie dann **Veröffentlichen**.

    ![Veröffentlichen][cache-publish-app]

2. Klicken Sie auf **Microsoft Azure-App-Verwaltungsdienst**.

    ![Veröffentlichen][cache-publish-to-app-service]

3. Wählen Sie das Abonnement, die zur Erstellung der Azure Ressourcen verwendet, erweitern Sie die Ressourcengruppe mit den Ressourcen, wählen Sie das gewünschte Web App aus und klicken Sie auf **OK**. Wenn Sie die Schaltfläche **Bereitstellen in Azure** Ihren Namen Web App mit **WebSite** gefolgt von denen nur einige zusätzlichen Zeichen beginnt verwendet.

    ![Wählen Sie Web App][cache-select-web-app]

4. Klicken Sie auf **Überprüfen Sie die Verbindung** zum Überprüfen der Einstellungen, und klicken Sie dann auf **Veröffentlichen**.

    ![Veröffentlichen][cache-publish]

    Nach kurzer Veröffentlichungsprozesses vervollständigt und ein Browser wird gestartet werden, mit der Ausführung Anwendung (Beispiel). Wenn Sie einen DNS-Fehler beim Prüfen oder Veröffentlichung erhalten und die Bereitstellung der Azure Ressourcen für die Anwendung wurde kürzlich erfolgreich abgeschlossen, warten Sie einen Moment, und versuchen Sie es erneut.

    ![Cache hinzugefügt][cache-added-to-application]

Die folgende Tabelle beschreibt die einzelnen Aktion links aus der Stichprobe Anwendung.

| Aktion                  | Beschreibung                                                                                                                                                      |
|-------------------------|------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| Neu erstellen              | Erstellen Sie ein neues Team.                                                                                                                                               |
| Jahreszeit wiedergeben             | Wiedergeben eine Jahreszeit Spiele, aktualisieren Sie das Team Stats und deaktivieren Sie veraltete Daten aus dem Cache der Teamwebsite.                                                                          |
| Cache löschen             | Deaktivieren Sie das Team Stats aus dem Cache.                                                                                                                             |
| Liste aus dem Cache         | Das Team Stats aus dem Cache abrufen. Ist eine Cache verpassen, laden Sie die Stats aus der Datenbank und in den Cache für eine erneute Verwendung speichern.                                        |
| Sortierten Satz aus dem Cache   | Abrufen der Teamwebsite Stats aus dem Cache mithilfe eines Satzes sortierten. Ist eine Cache verpassen, laden Sie die Stats aus der Datenbank, und mit einem sortierten Satz im Cache speichern.  |
| Top 5 Teams aus dem Cache  | Abrufen der obersten 5 Teams aus dem Cache mithilfe eines Satzes sortierten. Ist eine Cache verpassen, laden Sie die Stats aus der Datenbank, und mit einem sortierten Satz im Cache speichern. |
| Laden Sie aus der Datenbank            | Das Team Stats aus der Datenbank abrufen.                                                                                                                       |
| DB Quelltabelle              | Die Datenbank neu erstellen und mit Beispieldaten-Team erneut zu laden.                                                                                                        |
| Bearbeiten / Details / löschen | Bearbeiten eines Teams, Anzeigen von Details für ein Team, ein Team löschen.                                                                                                             |


Klicken Sie auf einige Aktionen, und probieren Sie die Daten aus verschiedenen Quellen abzurufen. Nicht die Unterschiede in der Zeitangabe dauert es die verschiedenen Optionen zum Abrufen von Daten aus der Datenbank und dem Cache.

## <a name="delete-the-resources-when-you-are-finished-with-the-application"></a>Wenn Sie mit der Anwendung fertig sind, löschen Sie die Ressourcen

Wenn Sie mit der Stichprobe zusammengehörenden Anwendung fertig sind, können Sie die Azure, um die Kosten und Ressourcen zu sparen verwendeten Ressourcen löschen. Wenn Sie die Schaltfläche **bereitstellen zu Azure** im Abschnitt [Azure Bereitstellungsressourcen](#provision-the-azure-resources) verwenden und alle Ihre Ressourcen in derselben Ressourcengruppe enthalten sind, können Sie diese zusammen in einem Vorgang löschen durch Löschen der Ressourcengruppe.

1. Melden Sie sich bei der [Azure-Portal](https://portal.azure.com) an, und klicken Sie auf **Ressourcengruppen**.
2. Geben Sie den Namen der Ressourcengruppe in das Textfeld zum **Filtern von Elementen...** ein.
3. Klicken Sie auf **...** rechts neben der Ressourcengruppe.
4. Klicken Sie auf **Löschen**.

    ![Löschen][cache-delete-resource-group]

5. Geben Sie den Namen der Ressourcengruppe ein, und klicken Sie auf **Löschen**.

    ![Löschen bestätigen][cache-delete-confirm]

Nach kurzer der Ressourcengruppe und alle enthaltenen Ressourcen gelöscht.

>[AZURE.IMPORTANT] Beachten Sie, dass das Löschen einer Ressourcengruppe nicht rückgängig gemacht werden kann und der Ressourcengruppe und alle Ressourcen endgültig gelöscht werden. Stellen Sie sicher, dass nicht versehentlich die falsche Ressourcengruppe oder Ressourcen zu löschen. Wenn Sie die Ressourcen für das Hosten in diesem Beispiel in eine vorhandene Ressourcengruppe erstellt haben, können Sie jede Ressource aus den jeweiligen Blades einzeln löschen.

## <a name="run-the-sample-application-on-your-local-machine"></a>Führen Sie die Beispiel-Anwendung auf dem lokalen Computer

Wenn Sie die Anwendung lokal auf Ihrem Computer ausführen, benötigen Sie eine Instanz Azure Redis Cache, in dem Sie Ihre Daten zwischenspeichern. 

-   Wenn Sie eine Anwendung in Azure veröffentlicht haben, wie im vorherigen Abschnitt beschrieben, können Sie die Redis Azure-Cache-Instanz aus, die in diesem Schritt bereitgestellt wurde.
-   Wenn Sie eine andere vorhandene Azure Redis Cache Instanz verfügen, können Sie, die in diesem Beispiel lokal ausführen verwenden.
-   Wenn Sie eine Instanz Azure Redis Cache erstellen müssen, folgen Sie die Schritten unter [Erstellen eines Cache](cache-dotnet-how-to-use-azure-redis-cache.md#create-a-cache).

Sobald Sie haben ausgewählt oder erstellt den Cache verwenden, navigieren Sie zu dem Cache Azure-Portal und abzurufen Sie [Hostname](cache-configure.md#properties) und [Tastenkombinationen](cache-configure.md#access-keys) für Ihren Cache. Anweisungen finden Sie unter [Einstellungen des Caches Redis konfigurieren](cache-configure.md#configure-redis-cache-settings).

1. Öffnen der `WebAppPlusCacheAppSecrets.config` Datei, die Sie beim [Konfigurieren der Anwendung Redis Cache verwenden](#configure-the-application-to-use-redis-cache) dieses Lernprogramms mit dem Editor Ihrer Wahl Schritt erstellt haben.

2. Bearbeiten der `value` Attribut und Ersetzen von `MyCache.redis.cache.windows.net` mit den [Hostnamen](cache-configure.md#properties) des Cache, und geben Sie entweder den [Primär-oder sekundäre](cache-configure.md#access-keys) Ihren Cache als das Kennwort.


        <appSettings>
          <add key="CacheConnection" value="MyCache.redis.cache.windows.net,abortConnect=false,ssl=true,password=..."/>
        </appSettings>


3. Drücken Sie **STRG + F5** , um die Anwendung ausführen.

>[AZURE.NOTE] Beachten Sie, dass Cache, da die Anwendung, einschließlich der Datenbank, die lokal ausgeführt wird und der Cache Redis in Azure gehostet wird, klicken Sie unter Ausführen die Datenbank angezeigt werden kann. Zur Optimierung der Systemleistung sollten Clientanwendung und Azure Redis Cache Instanz an derselben Stelle. 

## <a name="next-steps"></a>Nächste Schritte

-   Erfahren Sie mehr über die [Erste Schritte mit ASP.NET MVC 5](http://www.asp.net/mvc/overview/getting-started/introduction/getting-started) auf der Website [ASP.NET](http://asp.net/) .
-   Weitere Beispiele für das Erstellen einer ASP.NET Web App im App-Dienst, finden Sie unter [Erstellen und Bereitstellen einer ASP.NET Web-app in Azure-App-Verwaltungsdienst](https://github.com/Microsoft/HealthClinic.biz/wiki/Create-and-deploy-an-ASP.NET-web-app-in-Azure-App-Service) aus [HealthClinic.biz](https://github.com/Microsoft/HealthClinic.biz) 2015 verbinden [Demo](https://blogs.msdn.microsoft.com/visualstudio/2015/12/08/connectdemos-2015-healthclinic-biz/).
    -   Weitere Schnellstart aus HealthClinic.biz anschauen finden Sie unter [Azure Developer Tools Schnellstart](https://github.com/Microsoft/HealthClinic.biz/wiki/Azure-Developer-Tools-Quickstarts).
-   Weitere Informationen über das Verfahren mit [Code zuerst in eine neue Datenbank](https://msdn.microsoft.com/data/jj193542) zu Entität Framework, das in diesem Lernprogramm verwendet wird.
-   Weitere Informationen zu [Web apps in Azure-App-Dienst](../app-service-web/app-service-web-overview.md).
-   Erfahren Sie, wie Sie [Monitor](cache-how-to-monitor.md) Ihren Cache Azure-Portal.

-   Azure Redis Cache Premium Funktionen
    -   [Konfigurieren von Beibehaltung für einen Premium Azure Redis Cache](cache-how-to-premium-persistence.md)
    -   [So konfigurieren Sie für einen Premium Azure Redis Cache Cluster](cache-how-to-premium-clustering.md)
    -   [So konfigurieren Sie Virtual Network-Unterstützung für einen Premium Azure Redis Cache](cache-how-to-premium-vnet.md)
    -   Finden Sie weitere Details zum Größe, Durchsatz und Bandbreite mit Premium Caches der [Azure Redis Cache häufig gestellte Fragen](cache-faq.md#what-redis-cache-offering-and-size-should-i-use) .



<!-- IMAGES -->
[cache-starter-application]: ./media/cache-web-app-howto/cache-starter-application.png
[cache-added-to-application]: ./media/cache-web-app-howto/cache-added-to-application.png
[cache-create-project]: ./media/cache-web-app-howto/cache-create-project.png
[cache-select-template]: ./media/cache-web-app-howto/cache-select-template.png
[cache-model-add-class]: ./media/cache-web-app-howto/cache-model-add-class.png
[cache-model-add-class-dialog]: ./media/cache-web-app-howto/cache-model-add-class-dialog.png
[cache-add-controller]: ./media/cache-web-app-howto/cache-add-controller.png
[cache-add-controller-class]: ./media/cache-web-app-howto/cache-add-controller-class.png
[cache-configure-controller]: ./media/cache-web-app-howto/cache-configure-controller.png
[cache-global-asax]: ./media/cache-web-app-howto/cache-global-asax.png
[cache-RouteConfig-cs]: ./media/cache-web-app-howto/cache-RouteConfig-cs.png
[cache-layout-cshtml]: ./media/cache-web-app-howto/cache-layout-cshtml.png
[cache-layout-cshtml-code]: ./media/cache-web-app-howto/cache-layout-cshtml-code.png
[redis-cache-manage-nuget-menu]: ./media/cache-web-app-howto/redis-cache-manage-nuget-menu.png
[redis-cache-stack-exchange-nuget]: ./media/cache-web-app-howto/redis-cache-stack-exchange-nuget.png
[cache-teamscontroller]: ./media/cache-web-app-howto/cache-teamscontroller.png
[cache-web-config]: ./media/cache-web-app-howto/cache-web-config.png
[cache-views-teams-index-cshtml]: ./media/cache-web-app-howto/cache-views-teams-index-cshtml.png
[cache-teams-index-table]: ./media/cache-web-app-howto/cache-teams-index-table.png
[cache-status-message]: ./media/cache-web-app-howto/cache-status-message.png
[deploybutton]: ./media/cache-web-app-howto/deploybutton.png
[cache-deploy-to-azure-step-1]: ./media/cache-web-app-howto/cache-deploy-to-azure-step-1.png
[cache-deploy-to-azure-step-2]: ./media/cache-web-app-howto/cache-deploy-to-azure-step-2.png
[cache-deploy-to-azure-step-3]: ./media/cache-web-app-howto/cache-deploy-to-azure-step-3.png
[cache-deployment-started]: ./media/cache-web-app-howto/cache-deployment-started.png
[cache-publish-app]: ./media/cache-web-app-howto/cache-publish-app.png
[cache-publish-to-app-service]: ./media/cache-web-app-howto/cache-publish-to-app-service.png
[cache-select-web-app]: ./media/cache-web-app-howto/cache-select-web-app.png
[cache-publish]: ./media/cache-web-app-howto/cache-publish.png
[cache-delete-resource-group]: ./media/cache-web-app-howto/cache-delete-resource-group.png
[cache-delete-confirm]: ./media/cache-web-app-howto/cache-delete-confirm.png

