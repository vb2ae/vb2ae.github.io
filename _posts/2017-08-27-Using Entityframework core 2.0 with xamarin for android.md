# Using Entityframework core 2.0 with xamarin for android

In this post we are going to use the entity framework core 2.0 with a Xamarin for Android project





I am using Visual Studio 2017 (version 15.3)



I also installed .Net Core 2.0 from [https://dot.net](https://dot.net)



Once you have dot net core 2.0 installed which includes .net standard 2.0 lets start by creating a new Xamarin.Android project





First Create a Blank Xamarin for Android app



![Create Xamarin Android](/images/CreateAndroidApp.PNG)



Once that is added right click on the project and select Manage NuGet Package



Add the package microsoft.entityframeworkcore.sqlite


![Nuget](/images/NuGetEF.PNG)




Add the package and you will see it installs a few extra packages with it.  After it is installed I will update any packages that have updates available.






Lets add a Entities Folder to the android solution and create 2 code files Monkey.cs and MonkeyContext.cs





Monkey class



    public class Monkey

    {

            public int id { get; set; }

            public string monkeyType { get; set; }

     }





MonkeyContext class





    public class MonkeyContext : DbContext

    {

        private string DatabasePath { get; set; }

        public MonkeyContext(string databasePath)

        {

           DatabasePath = databasePath;

        }

        protected override void OnConfiguring(DbContextOptionsBuilder optionsBuilder)

        {

            optionsBuilder.UseSqlite($"Filename={DatabasePath}");

        }



        public DbSet<Monkey> Monkeys {get;set;}

    }










In the MainActivity  change the code in MainActivity to this. The code will create the database and add 5 monkeys to the database if there are not any records.  I also changed the MainActivity to inherit from ListActivity so it show the items in the database is a list





     public class MainActivity : ListActivity

    {

        MonkeyAdapter adapter;



        protected override async void OnCreate(Bundle savedInstanceState)

        {

            base.OnCreate(savedInstanceState);

            List<Monkey> lst = null;

            string path = Path.Combine(System.Environment.GetFolderPath(System.Environment.SpecialFolder.MyDocuments), "monkeys.db");

            using (var db = new MonkeyContext(path))

            {

                await db.Database.EnsureCreatedAsync();

                if (!db.Monkeys.Any())

                {

                    db.Monkeys.Add(new Monkey { monkeyType = "Squirrel Monkey" });

                    db.Monkeys.Add(new Monkey { monkeyType = "Spider Monkey" });

                    db.Monkeys.Add(new Monkey { monkeyType = "Golden Lion Tamarin" });

                    db.Monkeys.Add(new Monkey { monkeyType = "Howler Monkey" });

                    db.Monkeys.Add(new Monkey { monkeyType = "Owl or Night Monkey" });

                    await db.SaveChangesAsync();

                   

                }

                lst = db.Monkeys.ToList();

            }



            adapter = new MonkeyAdapter(this, lst);

            ListAdapter = adapter;

        }

    }



The code for MonkeyAdapter.   This code is needed to show the data in a list



     public class MonkeyAdapter : BaseAdapter<Monkey>

    {

        private readonly List<Monkey> data;

        private readonly Activity context;

        public MonkeyAdapter(Activity activity, IEnumerable<Monkey> monkeys)

        {

            data = monkeys.OrderBy(s => s.id).ToList();

            context = activity;

        }



        public override long GetItemId(int position)

        {

            return position;

        }



        public override Monkey this[int position]

        {

            get { return data[position]; }

        }



        public override int Count

        {

            get { return data.Count; }

        }



        public override View GetView(int position, View convertView, ViewGroup parent)

        {

           var view = convertView;

           if (view == null)

            {

                view = context.LayoutInflater.Inflate(Android.Resource.Layout.SimpleListItem1, null);

            }



            var monkey = data[position];

            var text = view.FindViewById<TextView>(Android.Resource.Id.Text1);

            text.Text = monkey.monkeyType;

            return view;

        }

    }


Once you run the project it will add a few items to the database and show them in a list view



![Android App](/images/AndroidEF.png)





You can download  a sample from my CodeImpact demo at GitHub



[https://github.com/vb2ae/CodeImpactNetStandard](https://github.com/vb2ae/CodeImpactNetStandard)











