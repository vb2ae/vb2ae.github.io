# WPF TabControl Binding Errors

Was looking at a Caliburn.Micro bug about getting an binding error while closing a window containing a tabcontrol with itemsource Conductor<IScreen>.Collection.OneActive without navigating to another tab.
  
https://github.com/Caliburn-Micro/Caliburn.Micro/issues/792
  
  Here is a link to repo that shows the issue.
  [https://github.com/to87al/DemoBug](https://github.com/to87al/DemoBug)
  
  ![App Start](/images/TabControlLaunchPage.png) 
  
  Open the window with a tab page
  
  ![Tab window opened](/images/OpenTabPageWindow.png) 
  
  Binding errors after closing the window without navigating to another tab
  
  ![Tab window opened](/images/TabWindowBindingErrors.png) 
  
  This is a result of a WPF bug.   There is a change you can make to the xaml to fix the binding error
  
    <Window.Resources>

    <Style x:Key="FixTabStripTabItemStyle" TargetType="{x:Type TabItem}"></Style>

    <ControlTemplate x:Key="FixTabStripTabItemControlTemplate" TargetType="{x:Type TabItem}">
        <Grid x:Name="templateRoot" SnapsToDevicePixels="True">
            <Border x:Name="mainBorder" BorderBrush="{TemplateBinding BorderBrush}" BorderThickness="1,1,1,0" Background="{TemplateBinding Background}" Margin="0">
                <Border x:Name="innerBorder" BorderBrush="#FFACACAC" BorderThickness="1,1,1,0" Background="White" Margin="-1" Opacity="0"/>
            </Border>
            <ContentPresenter x:Name="contentPresenter" ContentTemplate="{TemplateBinding HeaderTemplate}" Content="{TemplateBinding Header}" ContentStringFormat="{TemplateBinding HeaderStringFormat}" ContentSource="Header" Focusable="False" HorizontalAlignment="{Binding HorizontalContentAlignment, RelativeSource={RelativeSource FindAncestor, AncestorLevel=1, AncestorType={x:Type ItemsControl}}}" Margin="{TemplateBinding Padding}" RecognizesAccessKey="True" SnapsToDevicePixels="{TemplateBinding SnapsToDevicePixels}" VerticalAlignment="{Binding VerticalContentAlignment, RelativeSource={RelativeSource FindAncestor, AncestorLevel=1, AncestorType={x:Type ItemsControl}}}"/>
        </Grid>
        <ControlTemplate.Triggers>
            <MultiDataTrigger>
                <MultiDataTrigger.Conditions>
                    <Condition Binding="{Binding IsMouseOver, RelativeSource={RelativeSource Self}}" Value="true"/>
                    <Condition Binding="{Binding TabStripPlacement, RelativeSource={RelativeSource FindAncestor, AncestorLevel=1, AncestorType={x:Type TabControl}}}" Value="Left"/>
                </MultiDataTrigger.Conditions>
                <Setter Property="Background" TargetName="mainBorder">
                    <Setter.Value>
                        <LinearGradientBrush EndPoint="0,1" StartPoint="0,0">
                            <GradientStop Color="#FFECF4FC" Offset="0"/>
                            <GradientStop Color="#FFDCECFC" Offset="1"/>
                        </LinearGradientBrush>
                    </Setter.Value>
                </Setter>
                <Setter Property="BorderBrush" TargetName="mainBorder" Value="#FF7EB4EA"/>
                <Setter Property="BorderThickness" TargetName="innerBorder" Value="1,1,0,1"/>
                <Setter Property="BorderThickness" TargetName="mainBorder" Value="1,1,0,1"/>
            </MultiDataTrigger>
            <MultiDataTrigger>
                <MultiDataTrigger.Conditions>
                    <Condition Binding="{Binding IsMouseOver, RelativeSource={RelativeSource Self}}" Value="true"/>
                    <Condition Binding="{Binding TabStripPlacement, RelativeSource={RelativeSource FindAncestor, AncestorLevel=1, AncestorType={x:Type TabControl}}}" Value="Bottom"/>
                </MultiDataTrigger.Conditions>
                <Setter Property="Background" TargetName="mainBorder">
                    <Setter.Value>
                        <LinearGradientBrush EndPoint="0,1" StartPoint="0,0">
                            <GradientStop Color="#FFECF4FC" Offset="0"/>
                            <GradientStop Color="#FFDCECFC" Offset="1"/>
                        </LinearGradientBrush>
                    </Setter.Value>
                </Setter>
                <Setter Property="BorderBrush" TargetName="mainBorder" Value="#FF7EB4EA"/>
                <Setter Property="BorderThickness" TargetName="innerBorder" Value="1,0,1,1"/>
                <Setter Property="BorderThickness" TargetName="mainBorder" Value="1,0,1,1"/>
            </MultiDataTrigger>
            <MultiDataTrigger>
                <MultiDataTrigger.Conditions>
                    <Condition Binding="{Binding IsMouseOver, RelativeSource={RelativeSource Self}}" Value="true"/>
                    <Condition Binding="{Binding TabStripPlacement, RelativeSource={RelativeSource FindAncestor, AncestorLevel=1, AncestorType={x:Type TabControl}}}" Value="Right"/>
                </MultiDataTrigger.Conditions>
                <Setter Property="Background" TargetName="mainBorder">
                    <Setter.Value>
                        <LinearGradientBrush EndPoint="0,1" StartPoint="0,0">
                            <GradientStop Color="#FFECF4FC" Offset="0"/>
                            <GradientStop Color="#FFDCECFC" Offset="1"/>
                        </LinearGradientBrush>
                    </Setter.Value>
                </Setter>
                <Setter Property="BorderBrush" TargetName="mainBorder" Value="#FF7EB4EA"/>
                <Setter Property="BorderThickness" TargetName="innerBorder" Value="0,1,1,1"/>
                <Setter Property="BorderThickness" TargetName="mainBorder" Value="0,1,1,1"/>
            </MultiDataTrigger>
            <MultiDataTrigger>
                <MultiDataTrigger.Conditions>
                    <Condition Binding="{Binding IsMouseOver, RelativeSource={RelativeSource Self}}" Value="true"/>
                    <Condition Binding="{Binding TabStripPlacement, RelativeSource={RelativeSource FindAncestor, AncestorLevel=1, AncestorType={x:Type TabControl}}}" Value="Top"/>
                </MultiDataTrigger.Conditions>
                <Setter Property="Background" TargetName="mainBorder">
                    <Setter.Value>
                        <LinearGradientBrush EndPoint="0,1" StartPoint="0,0">
                            <GradientStop Color="#FFECF4FC" Offset="0"/>
                            <GradientStop Color="#FFDCECFC" Offset="1"/>
                        </LinearGradientBrush>
                    </Setter.Value>
                </Setter>
                <Setter Property="BorderBrush" TargetName="mainBorder" Value="#FF7EB4EA"/>
                <Setter Property="BorderThickness" TargetName="innerBorder" Value="1,1,1,0"/>
                <Setter Property="BorderThickness" TargetName="mainBorder" Value="1,1,1,0"/>
            </MultiDataTrigger>
            <MultiDataTrigger>
                <MultiDataTrigger.Conditions>
                    <Condition Binding="{Binding IsEnabled, RelativeSource={RelativeSource Self}}" Value="false"/>
                    <Condition Binding="{Binding TabStripPlacement, RelativeSource={RelativeSource FindAncestor, AncestorLevel=1, AncestorType={x:Type TabControl}}}" Value="Left"/>
                </MultiDataTrigger.Conditions>
                <Setter Property="Opacity" TargetName="contentPresenter" Value="0.56"/>
                <Setter Property="Background" TargetName="mainBorder" Value="#FFF0F0F0"/>
                <Setter Property="BorderBrush" TargetName="mainBorder" Value="#FFD9D9D9"/>
                <Setter Property="BorderThickness" TargetName="innerBorder" Value="1,1,0,1"/>
                <Setter Property="BorderThickness" TargetName="mainBorder" Value="1,1,0,1"/>
            </MultiDataTrigger>
            <MultiDataTrigger>
                <MultiDataTrigger.Conditions>
                    <Condition Binding="{Binding IsEnabled, RelativeSource={RelativeSource Self}}" Value="false"/>
                    <Condition Binding="{Binding TabStripPlacement, RelativeSource={RelativeSource FindAncestor, AncestorLevel=1, AncestorType={x:Type TabControl}}}" Value="Bottom"/>
                </MultiDataTrigger.Conditions>
                <Setter Property="Opacity" TargetName="contentPresenter" Value="0.56"/>
                <Setter Property="Background" TargetName="mainBorder" Value="#FFF0F0F0"/>
                <Setter Property="BorderBrush" TargetName="mainBorder" Value="#FFD9D9D9"/>
                <Setter Property="BorderThickness" TargetName="innerBorder" Value="1,0,1,1"/>
                <Setter Property="BorderThickness" TargetName="mainBorder" Value="1,0,1,1"/>
            </MultiDataTrigger>
            <MultiDataTrigger>
                <MultiDataTrigger.Conditions>
                    <Condition Binding="{Binding IsEnabled, RelativeSource={RelativeSource Self}}" Value="false"/>
                    <Condition Binding="{Binding TabStripPlacement, RelativeSource={RelativeSource FindAncestor, AncestorLevel=1, AncestorType={x:Type TabControl}}}" Value="Right"/>
                </MultiDataTrigger.Conditions>
                <Setter Property="Opacity" TargetName="contentPresenter" Value="0.56"/>
                <Setter Property="Background" TargetName="mainBorder" Value="#FFF0F0F0"/>
                <Setter Property="BorderBrush" TargetName="mainBorder" Value="#FFD9D9D9"/>
                <Setter Property="BorderThickness" TargetName="innerBorder" Value="0,1,1,1"/>
                <Setter Property="BorderThickness" TargetName="mainBorder" Value="0,1,1,1"/>
            </MultiDataTrigger>
            <MultiDataTrigger>
                <MultiDataTrigger.Conditions>
                    <Condition Binding="{Binding IsEnabled, RelativeSource={RelativeSource Self}}" Value="false"/>
                    <Condition Binding="{Binding TabStripPlacement, RelativeSource={RelativeSource FindAncestor, AncestorLevel=1, AncestorType={x:Type TabControl}}}" Value="Top"/>
                </MultiDataTrigger.Conditions>
                <Setter Property="Opacity" TargetName="contentPresenter" Value="0.56"/>
                <Setter Property="Background" TargetName="mainBorder" Value="#FFF0F0F0"/>
                <Setter Property="BorderBrush" TargetName="mainBorder" Value="#FFD9D9D9"/>
                <Setter Property="BorderThickness" TargetName="innerBorder" Value="1,1,1,0"/>
                <Setter Property="BorderThickness" TargetName="mainBorder" Value="1,1,1,0"/>
            </MultiDataTrigger>
            <MultiDataTrigger>
                <MultiDataTrigger.Conditions>
                    <Condition Binding="{Binding IsSelected, RelativeSource={RelativeSource Self}}" Value="false"/>
                    <Condition Binding="{Binding TabStripPlacement, RelativeSource={RelativeSource FindAncestor, AncestorLevel=1, AncestorType={x:Type TabControl}}}" Value="Left"/>
                </MultiDataTrigger.Conditions>
                <Setter Property="BorderThickness" TargetName="innerBorder" Value="1,1,0,1"/>
                <Setter Property="BorderThickness" TargetName="mainBorder" Value="1,1,0,1"/>
            </MultiDataTrigger>
            <MultiDataTrigger>
                <MultiDataTrigger.Conditions>
                    <Condition Binding="{Binding IsSelected, RelativeSource={RelativeSource Self}}" Value="true"/>
                    <Condition Binding="{Binding TabStripPlacement, RelativeSource={RelativeSource FindAncestor, AncestorLevel=1, AncestorType={x:Type TabControl}}}" Value="Left"/>
                </MultiDataTrigger.Conditions>
                <Setter Property="Panel.ZIndex" Value="1"/>
                <Setter Property="Margin" Value="-2,-2,0,-2"/>
                <Setter Property="Opacity" TargetName="innerBorder" Value="1"/>
                <Setter Property="BorderThickness" TargetName="innerBorder" Value="1,1,0,1"/>
                <Setter Property="BorderThickness" TargetName="mainBorder" Value="1,1,0,1"/>
            </MultiDataTrigger>
            <MultiDataTrigger>
                <MultiDataTrigger.Conditions>
                    <Condition Binding="{Binding IsSelected, RelativeSource={RelativeSource Self}}" Value="false"/>
                    <Condition Binding="{Binding TabStripPlacement, RelativeSource={RelativeSource FindAncestor, AncestorLevel=1, AncestorType={x:Type TabControl}}}" Value="Bottom"/>
                </MultiDataTrigger.Conditions>
                <Setter Property="BorderThickness" TargetName="innerBorder" Value="1,0,1,1"/>
                <Setter Property="BorderThickness" TargetName="mainBorder" Value="1,0,1,1"/>
            </MultiDataTrigger>
            <MultiDataTrigger>
                <MultiDataTrigger.Conditions>
                    <Condition Binding="{Binding IsSelected, RelativeSource={RelativeSource Self}}" Value="true"/>
                    <Condition Binding="{Binding TabStripPlacement, RelativeSource={RelativeSource FindAncestor, AncestorLevel=1, AncestorType={x:Type TabControl}}}" Value="Bottom"/>
                </MultiDataTrigger.Conditions>
                <Setter Property="Panel.ZIndex" Value="1"/>
                <Setter Property="Margin" Value="-2,0,-2,-2"/>
                <Setter Property="Opacity" TargetName="innerBorder" Value="1"/>
                <Setter Property="BorderThickness" TargetName="innerBorder" Value="1,0,1,1"/>
                <Setter Property="BorderThickness" TargetName="mainBorder" Value="1,0,1,1"/>
            </MultiDataTrigger>
            <MultiDataTrigger>
                <MultiDataTrigger.Conditions>
                    <Condition Binding="{Binding IsSelected, RelativeSource={RelativeSource Self}}" Value="false"/>
                    <Condition Binding="{Binding TabStripPlacement, RelativeSource={RelativeSource FindAncestor, AncestorLevel=1, AncestorType={x:Type TabControl}}}" Value="Right"/>
                </MultiDataTrigger.Conditions>
                <Setter Property="BorderThickness" TargetName="innerBorder" Value="0,1,1,1"/>
                <Setter Property="BorderThickness" TargetName="mainBorder" Value="0,1,1,1"/>
            </MultiDataTrigger>
            <MultiDataTrigger>
                <MultiDataTrigger.Conditions>
                    <Condition Binding="{Binding IsSelected, RelativeSource={RelativeSource Self}}" Value="true"/>
                    <Condition Binding="{Binding TabStripPlacement, RelativeSource={RelativeSource FindAncestor, AncestorLevel=1, AncestorType={x:Type TabControl}}}" Value="Right"/>
                </MultiDataTrigger.Conditions>
                <Setter Property="Panel.ZIndex" Value="1"/>
                <Setter Property="Margin" Value="0,-2,-2,-2"/>
                <Setter Property="Opacity" TargetName="innerBorder" Value="1"/>
                <Setter Property="BorderThickness" TargetName="innerBorder" Value="0,1,1,1"/>
                <Setter Property="BorderThickness" TargetName="mainBorder" Value="0,1,1,1"/>
            </MultiDataTrigger>
            <MultiDataTrigger>
                <MultiDataTrigger.Conditions>
                    <Condition Binding="{Binding IsSelected, RelativeSource={RelativeSource Self}}" Value="false"/>
                    <Condition Binding="{Binding TabStripPlacement, RelativeSource={RelativeSource FindAncestor, AncestorLevel=1, AncestorType={x:Type TabControl}}}" Value="Top"/>
                </MultiDataTrigger.Conditions>
                <Setter Property="BorderThickness" TargetName="innerBorder" Value="1,1,1,0"/>
                <Setter Property="BorderThickness" TargetName="mainBorder" Value="1,1,1,0"/>
            </MultiDataTrigger>
            <MultiDataTrigger>
                <MultiDataTrigger.Conditions>
                    <Condition Binding="{Binding IsSelected, RelativeSource={RelativeSource Self}}" Value="true"/>
                    <Condition Binding="{Binding TabStripPlacement, RelativeSource={RelativeSource FindAncestor, AncestorLevel=1, AncestorType={x:Type TabControl}}}" Value="Top"/>
                </MultiDataTrigger.Conditions>
                <Setter Property="Panel.ZIndex" Value="1"/>
                <Setter Property="Margin" Value="-2,-2,-2,0"/>
                <Setter Property="Opacity" TargetName="innerBorder" Value="1"/>
                <Setter Property="BorderThickness" TargetName="innerBorder" Value="1,1,1,0"/>
                <Setter Property="BorderThickness" TargetName="mainBorder" Value="1,1,1,0"/>
            </MultiDataTrigger>
        </ControlTemplate.Triggers>
    </ControlTemplate>
    </Window.Resources>
    <Grid>
       <TabControl x:Name="Items" Margin="5" d:ItemsSource="{d:SampleData ItemCount=4}" ItemContainerStyle="{StaticResource FixTabStripTabItemStyle}" />
    </Grid>
  
  
  Reference 
  
  
  [https://stackoverflow.com/questions/14419248/cannot-find-source-for-binding](https://stackoverflow.com/questions/14419248/cannot-find-source-for-binding)
  

