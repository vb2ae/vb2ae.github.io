Here is an example on how to clone an object in a portable class library



I am using Json.net to help.  Add the Json.Net nuget package to any project in the solution that uses the PCL


![Nuget](/images/NuGetNewtonsoft.png) 




Then you an serialize the object into Json and then deserialize it right away to create a clone of a object





        public T CloneObject<T>(T toBeCloned)

        {

            T clone = default(T);

            string serialized = JsonConvert.SerializeObject(toBeCloned);

            clone = JsonConvert.DeserializeObject<T>(serialized);

            return clone;

        }
