# Visual Studio 2017 live unit tests

I was experimenting today with VS 2017 live unit testing. I really like them a lot. I wish they were available in all editions of VS  2017 not just enterprise.



I started with a simple console app.  Which adds 2 numbers.





   public class Program

    {

        static void Main(string[] args)

        {

            Console.Write("1 + 1 = ");

            Console.WriteLine(Add2Numbers(1,1).ToString());

            Console.WriteLine("Press any key to continue");

            Console.ReadLine();

        }

        public static int Add2Numbers(int x,int y)

        {

            return x * y;

        }

    }





Then I added a Unit Test project. I added a project reference to my ConsoleApp





Here is the tests I added.


   
     Namespace UnitTestProject1

     {

    [TestClass]

    public class UnitTest1

    {

        [TestMethod]

        public void TestMethod1()

        {

            int x = 1;

            int y = 1;

            int expected = 2;

            Assert.AreEqual(expected, ConsoleApp1.Program.Add2Numbers(x, y));

        }

    }

    }





Then I build the project and ran the test.  As you can see the test failed. 



Lets turn on the Live Unit Tests in Visual Studio's Options.  There is a section for it.

![Live Unit test settings](/images/LiveUnitTestSettings.png)






Right click on the solution in the solution explorer and select Live Tests and select include.



Here is what you will see.


![Unit test fail](/images/LiveUnitTestFail.png)





Now if we update the code. We  will see it goes to passing







        public static int Add2Numbers(int x,int y)

        {

            return x + y;

        }




![Unit Test Pass](/images/LiveUnitTestPass.png)




Very useful feature.
















