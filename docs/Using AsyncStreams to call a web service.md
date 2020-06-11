# .Net Core 3.0 includes Asynchronous streams.

Basically IAsyncEnumerable<T> is an asynchronous version of IEnumerable<T>.   To use it in a you await a foreach loop to consume the elements

    await foreach (var location in GetISSLocationSequence())
    {
        Console.WriteLine(location);
    }
    
    
GetISSLocationSequence is an async function which yield 20 IIS locations. It waits 1 second between getting locations


    Public static async System.Collections.Generic.IAsyncEnumerable<string> GetISSLocationSequence()
    {
        using HttpClient http = new HttpClient();
        for (int i = 0; i < 20; i++)
        {
           var json = await http.GetStringAsync("http://api.open-notify.org/iss-now.json");
           await Task.Delay(2000);
           yield return json;
        }
    }
    
    
One other thing I would like to point out was the format for the using 
statement.  Notice in this function I am using a using statement to make 
sure the HtppClient get disposed of when we done with it.  Notice we no 
long have to put the code is {}.  The HttpClient will dispose at the end 
of the function

To demo this I put the code in a .net core console application.  To allow 

await in the sub main I changed it from a void to async Task



    class Program
    {
        static async Task Main(string[] args)
        {
  
             await foreach (var location in GetISSLocationSequence())
             {
                 Console.WriteLine(location);
             }
        }
