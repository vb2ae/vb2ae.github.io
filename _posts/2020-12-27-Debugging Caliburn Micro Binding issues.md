# Debugging Caliburn Micro Binding issues

I was looking at this Caliburn Micro question on stackoverflow

https://stackoverflow.com/questions/65362824/datagrid-column-binding-to-class

One thing you can do in Caliburn.Micro to see what is going on with the Binding is to add a logger. This class inherits from ILog to write to the console window.

    public class DebuggingLogger : ILog
    {
        #region Fields
        private readonly Type _type;
        #endregion

        #region Constructors
        public DebuggingLogger(Type type)
        {
            _type = type;
        }
        #endregion

        #region Helper Methods
        private string CreateLogMessage(string format, params object[] args)
        {
            return string.Format("[{0}] {1}",
                DateTime.Now.ToString("o"),
                string.Format(format, args));
        }
        #endregion

        #region ILog Members
        public void Error(Exception exception)
        {
            Debug.WriteLine(CreateLogMessage(exception.ToString()), "ERROR");
        }

        public void Info(string format, params object[] args)
        {
            Debug.WriteLine(CreateLogMessage(format, args), "INFO");
        }

        public void Warn(string format, params object[] args)
        {
            Debug.WriteLine(CreateLogMessage(format, args), "WARN");
        }
        #endregion
    }


To use it in the Bootstapper contractor register the logger.

        public Bootstrapper()
        {
            Initialize();
             LogManager.GetLog = type => new DebuggingLogger(type);
        }
        
        
 Now when you run the app you see info on what is going on in the output window with the bindings
 
    INFO: [2020-12-27T11:25:18.7057010-05:00] Action Convention Not Applied: No actionable element for Set.
    INFO: [2020-12-27T11:25:18.7088303-05:00] Action Convention Not Applied: No actionable element for GetType.
    INFO: [2020-12-27T11:25:18.7120732-05:00] Action Convention Not Applied: No actionable element for ToString.
    INFO: [2020-12-27T11:25:18.7157657-05:00] Action Convention Not Applied: No actionable element for Equals.
    INFO: [2020-12-27T11:25:18.7195581-05:00] Action Convention Not Applied: No actionable element for GetHashCode.
    INFO: [2020-12-27T11:25:18.7338489-05:00] ItemTemplate applied to Products.
    INFO: [2020-12-27T11:25:18.7375857-05:00] Binding Convention Applied: Element Products.
    INFO: [2020-12-27T11:25:18.7412851-05:00] Activating StackOverFlowQuestion.ViewModels.HomeViewModel.
    'StackOverFlowQuestion.exe' (CoreCLR: clrhost): Loaded 'C:\Program Files\dotnet\shared\Microsoft.NETCore.App\3.1.10\System.Drawing.Primitives.dll'. 
    'StackOverFlowQuestion.exe' (CoreCLR: clrhost): Loaded 'C:\Program Files\dotnet\shared\Microsoft.WindowsDesktop.App\3.1.10\PresentationFramework-SystemCore.dll'. 
    INFO: [2020-12-27T11:25:26.1121474-05:00] Deactivating StackOverFlowQuestion.ViewModels.ShellViewModel.
    INFO: [2020-12-27T11:25:26.1639366-05:00] Closed StackOverFlowQuestion.ViewModels.ShellViewModel.
    The program '[21804] StackOverFlowQuestion.exe' has exited with code 0 (0x0).

If there is an error you will see something like this

    INFO: [2020-12-27T11:27:53.9732043-05:00] ItemTemplate applied to Products.
    INFO: [2020-12-27T11:27:53.9814484-05:00] Binding Convention Applied: Element Products.
    INFO: [2020-12-27T11:27:53.9864779-05:00] Activating StackOverFlowQuestion.ViewModels.HomeViewModel.
    'StackOverFlowQuestion.exe' (CoreCLR: clrhost): Loaded 'C:\Program Files\dotnet\shared\Microsoft.NETCore.App\3.1.10\System.Drawing.Primitives.dll'. 
    'StackOverFlowQuestion.exe' (CoreCLR: clrhost): Loaded 'C:\Program Files\dotnet\shared\Microsoft.WindowsDesktop.App\3.1.10\PresentationFramework-SystemCore.dll'. 
    System.Windows.Data Error: 40 : BindingExpression path error: 'ProductLotNumber2' property not found on 'object' ''ProductModel' (HashCode=7421470)'. BindingExpression:Path=ProductLotNumber2; DataItem='ProductModel' (HashCode=7421470); target element is 'TextBlock' (Name=''); target property is 'Text' (type 'String')
    The program '[20584] StackOverFlowQuestion.exe' has exited with code -1 (0xffffffff).
    
    
   You can find a repo with some sample code here 
   https://github.com/vb2ae/StackOverFlowQuestion
   



