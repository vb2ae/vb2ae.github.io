# Xamarin Android Multiline label not working properly

I was having an issue with getting a Label to multiline in an Xamarin forms ListView in an android app.



My XAML was this



<ContentPage xmlns="http://xamarin.com/schemas/2014/forms"
             xmlns:x="http://schemas.microsoft.com/winfx/2009/xaml"
             x:Class="XamarinDev.BlogPage">
    <ListView ItemsSource="{Binding BlogPosts}" >
        <ListView.ItemTemplate>
            <DataTemplate>
                <ViewCell>
                    <StackLayout Padding="15,0" HorizontalOptions="Fill" VerticalOptions="StartAndExpand" >
                        <Label Text="{Binding Title}" FontAttributes="Bold" LineBreakMode="WordWrap"/>
                        <Label Text="{Binding Description}" LineBreakMode="WordWrap"></Label>
                    </StackLayout>
                </ViewCell>
            </DataTemplate>
        </ListView.ItemTemplate>
    </ListView>


And it looked like this


![Multiline listview lines not working properly](/images/AndroidListview.png)






After I added HasUnevenRows="True" to the listview I got much better results



    <ListView ItemsSource="{Binding BlogPosts}" HasUnevenRows="True">
        <ListView.ItemTemplate>
            <DataTemplate>
                <ViewCell>
                    <StackLayout Padding="15,0" HorizontalOptions="Fill" VerticalOptions="StartAndExpand" >
                        <Label Text="{Binding Title}" FontAttributes="Bold" LineBreakMode="WordWrap"/>
                        <Label Text="{Binding Description}" LineBreakMode="WordWrap"></Label>
                    </StackLayout>
                </ViewCell>
            </DataTemplate>
        </ListView.ItemTemplate>
    </ListView>



![Fixed multiline listview label](/images/AndroidListViewAfter.png)


