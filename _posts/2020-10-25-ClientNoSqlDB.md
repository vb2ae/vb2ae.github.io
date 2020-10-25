# ClientNoSQLDb


For this hacktoberfest I updated the ClientNoSQLDb project.  For this release I optimized the code a little and updated the samples.  I also changed the unit tests to use XUnit.  I like that unit testing framework better than NUint.

I updated the NuGet package to version 1.0

Here is a quick sample of using the ClientNoSQLDB in a console app.  Please note this is meant to be used as a database to a local app (Xamarin, windows, or console app for example).  This is not meant to be server side database to be used with a website.

Here is quick example on how to use the database.

           List<Person> list;
            using (var db = new ClientNoSqlDB.DbInstance("testing"))
            {
                db.Map<Person>().Automap(i => i.Id);
                db.Initialize();
                list = db.LoadAll<Person>().ToList();
                if (list != null && !list.Any())
                {
                    db.Save(new Person() { FirstName = "Ken", Id = 1, LastName = "Tucker" },
                    new Person() { FirstName = "Tony", Id = 2, LastName = "Stark" },
                    new Person() { FirstName = "John", Id = 3, LastName = "Papa" },
                    new Person() { FirstName = "Delete", Id = 4, LastName = "Me" });
                }
                var item = db.LoadByKey<Person>(4);
                if (item != null)
                {
                    db.Delete<Person>(item);
                }
                list = db.LoadAll<Person>().ToList();

                foreach(var p in list)
                {
                    Console.WriteLine($"{p.FirstName} {p.LastName}");
                }
            }


In this example we create a database and add an index to make looking up items quicker. 

We inserted 4 items to the database and deleted one.  The second time the app was run when we load the items we see we still have the ones added.

