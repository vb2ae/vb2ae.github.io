# Guard Methods in Caliburn Micro

i have been working on fixing some of the Caliburn.Micro bugs recently.  

One of the bugs was talking about the Guard Methods not firing correctly.

There are multiple ways to bind a method in your View model to a button click event for example.


            <Button Text="{Binding Delta}" x:Name="ButtonDelta">
                <Button.Triggers>
                    <EventTrigger Event="Clicked">
                        <cm:ActionMessage MethodName="CountUp" AssociatedObject="{x:Reference ButtonDelta}" >
                            <cm:Parameter Value="{Binding Source={x:Reference Count}, Path=Text}"/>
                        </cm:ActionMessage>
                    </EventTrigger>
                </Button.Triggers>
            </Button>
            
            
 In this example we add an Action Message which is tells the button call a method called CountUp when the button is pressed.
 
 Guard methods will fire before the click method to make sure it is ok to run the button click event.  To add a Guard Method to add a method that starts with Casn before the click event method name.  So for this example the method name is CanCountUp.
 
         public bool CanCountUp(int i)
        {
            if (i > 10)
                return false;

            if (Count < 10)
                return true;
            else
                return false;
        }
        
 
 One thing you need to do is in the ViewModels constructor enable EnforceGuardsDuringInvocation 
 
         public MainViewModel()
        {
            ActionMessage.EnforceGuardsDuringInvocation = true;
        }
        
 There is a complete example located here
 
 https://github.com/vb2ae/Guard.Bug
 
 
 
