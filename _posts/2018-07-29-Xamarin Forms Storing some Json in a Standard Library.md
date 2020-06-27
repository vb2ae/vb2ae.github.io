# Xamarin Forms Storing some Json in a Standard Library

In one of my Xamarin forms app I wanted to include some default data for the app in Json format.



Rather than create a web service to load the data on the first run I went ahead and created a Json file to include the default data.



     [

           {"Question":"Name two key components that make up Sitecore XP","Answer":"Experience CMS, and marketing platform"}


      etc...



I added the Json file to my Xamarin Forms standard library and set its build action to embedded resource

![Solution Explorer](/images/SolutionExplorer.png) 

![properties window](/images/JsonProperties.png) 

To extract the data I used a function like this.



        public ObservableCollection<QuestionPair> GetQuestions()
        {
            var assembly = typeof(DataService).GetTypeInfo().Assembly;
            Stream stream = assembly.GetManifestResourceStream("SitecoreFlashCards.questions.json");
            StreamReader streamReader = new StreamReader(stream);
            string json = streamReader.ReadToEnd();
            ObservableCollection<QuestionPair> questions = new ObservableCollection<QuestionPair>();
            var list = Newtonsoft.Json.JsonConvert.DeserializeObject<List<QuestionPair>>(json);
            foreach(var item in list)
            {
                questions.Add(item);
            }

            return questions;
        }



First I created a stream so I can access the Json file in the standard library.  The I used a stream reader to get the text from the file and deserialize it with Json.net



The path to the resource is the class library default namespace and the path to the file and file name in the dll.



Replace DataService with the name of the class you are trying to get the Json file from.



