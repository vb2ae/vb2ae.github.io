# Asp.Net Core 2 Configuration Values

In this blog post I will show you how to access the site settings in an asp.net core 2.0 website.  I am using Visual Studio for the Mac to doing the coding but it should work the same in the windows version of Visual Studio.



Configuration values are store in the file appsettings.json.   It is a json based configuration file.  An example file could look something like this.



     {
          "NumberOfItemsToShow": 20,
          "Title": "Demo Application",
          "Topics": ["Asp.net","Asp.net core", ".net core", "Xamarin"],
          "Logging": {
                "IncludeScopes": false,
                "LogLevel": {
                "Default": "Warning"
                 }
     }



In asp.net you stored your app settings in a file called web.config.  If you wanted different values for different environments you wrote a config transform to change the value for that environment.  In asp.net core you create a appsettings.[environment name].json to overwrite values for the other environment.



To start off we are going to create a class to hold our config values.  I am going to call it SiteSettings.


      using System;
      using System.Collections.Generic;
      namespace SettingsDemo.Models
      {
            public class SiteSettings
           {
                 public int NumberOfItemsToShow { get; set; }
                 public string Title { get; set; }

                 public List<string> Topics { get; set; }
           }
      }


Now in the file startup.cs we need to update the startup function to get the hosting environment and load the config values.


        private readonly IHostingEnvironment hostingEnvironment;


        public Startup(IHostingEnvironment env, IConfiguration config)
        {
            var builder = new ConfigurationBuilder()
               .SetBasePath(env.ContentRootPath)
               .AddJsonFile("appsettings.json", optional: false, reloadOnChange: true)
               .AddJsonFile($"appsettings.{env.EnvironmentName}.json", optional: true)
               .AddEnvironmentVariables(); 
            hostingEnvironment = env;
            Configuration = config;
        }


To load the setting we need to change the Configure Service method.



        // This method gets called by the runtime. Use this method to add services to the container.
        public void ConfigureServices(IServiceCollection services)
        {
            services.Configure<SiteSettings>(Configuration);
            services.AddMvc();
        }


Finally we need to use dependency injection to get access to them in the controller we need to use them in.



        private SiteSettings siteSettings;

        public HomeController(IOptions<SiteSettings> settings)
        {
            siteSettings = settings.Value;
            
        }


Hope this helps


You can find the sample code on GitHub


https://github.com/vb2ae/AspNetCoreConfiguration
