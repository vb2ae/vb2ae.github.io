# Visual Studio for Mac MSTests project wont load

I opened a Xamarin Forms project I created on a windows pc with visual studio for Mac.






![Unit Test Project](/images/UnitTestProject.png)




Besides the UWP version of the app not being able to load the MS Tests unit tests could not be loaded either.  Since I really need the unit tests to run I edited the project so it would work.



This is the original



     <?xml version="1.0" encoding="utf-8"?>

     <Project ToolsVersion="15.0" DefaultTargets="Build" xmlns="http://schemas.microsoft.com/developer/msbuild/2003">

     <Import Project="..\packages\MSTest.TestAdapter.1.2.0\build\net45\MSTest.TestAdapter.props" Condition="Exists('..\packages\MSTest.TestAdapter.1.2.0\build\net45\MSTest.TestAdapter.props')" />

     <PropertyGroup>

     <Configuration Condition=" '$(Configuration)' == '' ">Debug</Configuration>

     <Platform Condition=" '$(Platform)' == '' ">AnyCPU</Platform>

     <ProjectGuid>{11CF56D3-607A-4251-B491-E88D59114CFE}</ProjectGuid>

     <OutputType>Library</OutputType>

     <AppDesignerFolder>Properties</AppDesignerFolder>

     <RootNamespace>App4.test</RootNamespace>

     <AssemblyName>App4.test</AssemblyName>

     <TargetFrameworkVersion>v4.6.1</TargetFrameworkVersion>

     <FileAlignment>512</FileAlignment>

     <ProjectTypeGuids>{3AC096D0-A1C2-E12C-1390-A8335801FDAB};{FAE04EC0-301F-11D3-BF4B-00C04F79EFBC}</ProjectTypeGuids>

     <VisualStudioVersion Condition="'$(VisualStudioVersion)' == ''">15.0</VisualStudioVersion>

     <VSToolsPath Condition="'$(VSToolsPath)' == ''">$(MSBuildExtensionsPath32)\Microsoft\VisualStudio\v$(VisualStudioVersion)</VSToolsPath>

     <ReferencePath>$(ProgramFiles)\Common Files\microsoft shared\VSTT\$(VisualStudioVersion)\UITestExtensionPackages</ReferencePath>

     <IsCodedUITest>False</IsCodedUITest>

    <TestProjectType>UnitTest</TestProjectType>

    <NuGetPackageImportStamp>

    </NuGetPackageImportStamp>

    </PropertyGroup>

    <PropertyGroup Condition=" '$(Configuration)|$(Platform)' == 'Debug|AnyCPU' ">

    <DebugSymbols>true</DebugSymbols>

    <DebugType>full</DebugType>

    <Optimize>false</Optimize>

    <OutputPath>bin\Debug\</OutputPath>

    <DefineConstants>DEBUG;TRACE</DefineConstants>

    <ErrorReport>prompt</ErrorReport>

    <WarningLevel>4</WarningLevel>

    </PropertyGroup>

    <PropertyGroup Condition=" '$(Configuration)|$(Platform)' == 'Release|AnyCPU' ">

    <DebugType>pdbonly</DebugType>

    <Optimize>true</Optimize>

    <OutputPath>bin\Release\</OutputPath>

    <DefineConstants>TRACE</DefineConstants>

    <ErrorReport>prompt</ErrorReport>

    <WarningLevel>4</WarningLevel>

    </PropertyGroup>

    <ItemGroup>

    <Reference Include="Microsoft.VisualStudio.TestPlatform.TestFramework, Version=14.0.0.0, Culture=neutral, PublicKeyToken=b03f5f7f11d50a3a, processorArchitecture=MSIL">

    <HintPath>..\packages\MSTest.TestFramework.1.2.0\lib\net45\Microsoft.VisualStudio.TestPlatform.TestFramework.dll</HintPath>

    </Reference>

    <Reference Include="Microsoft.VisualStudio.TestPlatform.TestFramework.Extensions, Version=14.0.0.0, Culture=neutral, PublicKeyToken=b03f5f7f11d50a3a, processorArchitecture=MSIL">

    <HintPath>..\packages\MSTest.TestFramework.1.2.0\lib\net45\Microsoft.VisualStudio.TestPlatform.TestFramework.Extensions.dll</HintPath>

    </Reference>

    <Reference Include="System" />

    <Reference Include="System.Core" />

    </ItemGroup>

    <ItemGroup>

    <Compile Include="UnitTest1.cs" />

    <Compile Include="Properties\AssemblyInfo.cs" />

    </ItemGroup>

    <ItemGroup>

    <None Include="packages.config" />

    </ItemGroup>

    <Import Project="$(VSToolsPath)\TeamTest\Microsoft.TestTools.targets" Condition="Exists('$(VSToolsPath)\TeamTest\Microsoft.TestTools.targets')" />

    <Import Project="$(MSBuildToolsPath)\Microsoft.CSharp.targets" />

    <Target Name="EnsureNuGetPackageBuildImports" BeforeTargets="PrepareForBuild">

    <PropertyGroup>

    <ErrorText>This project references NuGet package(s) that are missing on this computer. Use NuGet Package Restore to download them.  For more information, see http://go.microsoft.com/fwlink/?LinkID=322105. The missing file is {0}.</ErrorText>

    </PropertyGroup>

    <Error Condition="!Exists('..\packages\MSTest.TestAdapter.1.2.0\build\net45\MSTest.TestAdapter.props')" Text="$([System.String]::Format('$(ErrorText)', '..\packages\MSTest.TestAdapter.1.2.0\build\net45\MSTest.TestAdapter.props'))" />

    <Error Condition="!Exists('..\packages\MSTest.TestAdapter.1.2.0\build\net45\MSTest.TestAdapter.targets')" Text="$([System.String]::Format('$(ErrorText)', '..\packages\MSTest.TestAdapter.1.2.0\build\net45\MSTest.TestAdapter.targets'))" />

    </Target>

    <Import Project="..\packages\MSTest.TestAdapter.1.2.0\build\net45\MSTest.TestAdapter.targets" Condition="Exists('..\packages\MSTest.TestAdapter.1.2.0\build\net45\MSTest.TestAdapter.targets')" />

    </Project>



I changed the project to a dot net core unit test project by editing the project file.  Here is what I changed it to.  The updated test project uses MS Test V2





      <Project Sdk="Microsoft.NET.Sdk">

        <PropertyGroup>
            <TargetFramework>netcoreapp2.0</TargetFramework>

        <IsPackable>false</IsPackable>
       </PropertyGroup>

      <ItemGroup>
         <PackageReference Include="Microsoft.NET.Test.Sdk" Version="15.3.0-preview-20170628-02" />
         <PackageReference Include="MSTest.TestAdapter" Version="1.1.18" />
         <PackageReference Include="MSTest.TestFramework" Version="1.1.18" />
      </ItemGroup>

  <ItemGroup>
    <ProjectReference Include="..\App4\App4\App4.csproj" />
  </ItemGroup>
</Project>