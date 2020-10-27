# Astronomy Picuture of the Day

Durring the 2020 HacktoberFest I updated the Astronomy Picture of the Day class library.  I added the ability to get pictures from the Mars Rovers.

The library now has 2 methods GetTodaysPictureAsync and GetMarsPictureAsync. These methods allow you to get pictures from Nasa from one of the mars rovers or there astronomy picture of the day.

You will need an api key from the Nasa website to use the apis. You can get a key at https://api.nasa.gov/

The Nuget Package to install is AstronomyPictureOfTheDay
https://www.nuget.org/packages/AstronomyPictureTheDay/0.9.0

# To get a picture from one of the Mars Rovers

                response = await marsPictureOfTheDay.GetMarsPictureAsync(RoverEnum.Curiosity, DateTime.Now.AddDays(-7),"DEMO_KEY");
                if (response != null)
                {
                    if (response.Success)
                    {
                        Title = response.picturesFromMars.photos[0].camera.full_name;
                        PictureOfDay = response.picturesFromMars.photos[0].img_src;
                    }
                }
                
Replace "DEMO_KEY" with your key from Nasa.

This example will get the a picture from the Mars Curiosity rover from a week ago.  

Note the Opportunity rover was only operational from 1/25/2004 to 7/10/2018
The Curiosity rover landed 8/6/2012


# To get the Astronomy Picture of the Day

                response = await apod.GetTodaysPictureAsync("DEMO_KEY");
                if (response != null)
                {
                    if (response.Success)
                    {
                        Title = response.pictureOfTheDay.title;
                        PictureOfDay = response.pictureOfTheDay.url;
                    }
                }
                
