# Learing F# Xamarin.Android ListView

I am learning F# and decided I would start with a Xamarin.Android project that shows a list view.   

I decided I would convert the c# example in Mirosoft docs to F#.

https://docs.microsoft.com/en-us/xamarin/android/user-interface/layouts/list-view/


I started with a Xamarin.Android blank project with F# as the language

Please all the instructions for adding xml files.

In MainActivity.fs change the class to inherit from ListActivity from Activity


     type MainActivity () =
         inherit ListActivity ()
         
         
In the MainActivity.fs we want to change the OnCreate function.  First have it create a list of countries.


       override this.OnCreate (bundle) =
         base.OnCreate (bundle)
         let countries = [ "Afghanistan";"Albania";"Algeria";"American Samoa";"Andorra";
              "Angola";"Anguilla";"Antarctica";"Antigua and Barbuda";"Argentina";
              "Armenia";"Aruba";"Australia";"Austria";"Azerbaijan";
              "Bahrain";"Bangladesh";"Barbados";"Belarus";"Belgium";
              "Belize";"Benin";"Bermuda";"Bhutan";"Bolivia";
              "Bosnia and Herzegovina";"Botswana";"Bouvet Island";"Brazil";"British Indian Ocean Territory";
              "British Virgin Islands";"Brunei";"Bulgaria";"Burkina Faso";"Burundi";
              "Cote d'Ivoire";"Cambodia";"Cameroon";"Canada";"Cape Verde";
              "Cayman Islands";"Central African Republic";"Chad";"Chile";"China";
              "Christmas Island";"Cocos (Keeling) Islands";"Colombia";"Comoros";"Congo";
              "Cook Islands";"Costa Rica";"Croatia";"Cuba";"Cyprus";"Czech Republic";
              "Democratic Republic of the Congo";"Denmark";"Djibouti";"Dominica";"Dominican Republic";
              "East Timor";"Ecuador";"Egypt";"El Salvador";"Equatorial Guinea";"Eritrea";
              "Estonia";"Ethiopia";"Faeroe Islands";"Falkland Islands";"Fiji";"Finland";
              "Former Yugoslav Republic of Macedonia";"France";"French Guiana";"French Polynesia";
              "French Southern Territories";"Gabon";"Georgia";"Germany";"Ghana";"Gibraltar";
              "Greece";"Greenland";"Grenada";"Guadeloupe";"Guam";"Guatemala";"Guinea";"Guinea-Bissau";
              "Guyana";"Haiti";"Heard Island and McDonald Islands";"Honduras";"Hong Kong";"Hungary";
              "Iceland";"India";"Indonesia";"Iran";"Iraq";"Ireland";"Israel";"Italy";"Jamaica";
              "Japan";"Jordan";"Kazakhstan";"Kenya";"Kiribati";"Kuwait";"Kyrgyzstan";"Laos";
              "Latvia";"Lebanon";"Lesotho";"Liberia";"Libya";"Liechtenstein";"Lithuania";"Luxembourg";
              "Macau";"Madagascar";"Malawi";"Malaysia";"Maldives";"Mali";"Malta";"Marshall Islands";
              "Martinique";"Mauritania";"Mauritius";"Mayotte";"Mexico";"Micronesia";"Moldova";
              "Monaco";"Mongolia";"Montserrat";"Morocco";"Mozambique";"Myanmar";"Namibia";
              "Nauru";"Nepal";"Netherlands";"Netherlands Antilles";"New Caledonia";"New Zealand";
              "Nicaragua";"Niger";"Nigeria";"Niue";"Norfolk Island";"North Korea";"Northern Marianas";
              "Norway";"Oman";"Pakistan";"Palau";"Panama";"Papua New Guinea";"Paraguay";"Peru";
              "Philippines";"Pitcairn Islands";"Poland";"Portugal";"Puerto Rico";"Qatar";
              "Reunion";"Romania";"Russia";"Rwanda";"Sqo Tome and Principe";"Saint Helena";
              "Saint Kitts and Nevis";"Saint Lucia";"Saint Pierre and Miquelon";
              "Saint Vincent and the Grenadines";"Samoa";"San Marino";"Saudi Arabia";"Senegal";
              "Seychelles";"Sierra Leone";"Singapore";"Slovakia";"Slovenia";"Solomon Islands";
              "Somalia";"South Africa";"South Georgia and the South Sandwich Islands";"South Korea";
              "Spain";"Sri Lanka";"Sudan";"Suriname";"Svalbard and Jan Mayen";"Swaziland";"Sweden";
              "Switzerland";"Syria";"Taiwan";"Tajikistan";"Tanzania";"Thailand";"The Bahamas";
              "The Gambia";"Togo";"Tokelau";"Tonga";"Trinidad and Tobago";"Tunisia";"Turkey";
              "Turkmenistan";"Turks and Caicos Islands";"Tuvalu";"Virgin Islands";"Uganda";
              "Ukraine";"United Arab Emirates";"United Kingdom";
              "United States";"United States Minor Outlying Islands";"Uruguay";"Uzbekistan";
              "Vanuatu";"Vatican City";"Venezuela";"Vietnam";"Wallis and Futuna";"Western Sahara";
              "Yemen";"Yugoslavia";"Zambia";"Zimbabwe"]
          // Set our view from the "main" layout resource
         let countyList = new System.Collections.Generic.List<string>()
         countyList.AddRange(countries)
  
  
         
 Then we create an ArrayAdapter from the list of countries
 
      let adapter = new ArrayAdapter(this.BaseContext, Resources.Layout.list_item, countyList)
      this.ListAdapter <- adapter
      
 We should also turn on the ListView's TextFilter
 
     this.ListView.TextFilterEnabled <- true
 
 
 Then finally we can add the eventhandler to show a toast message of the item clicked
 
      this.ListView.ItemClick.Add(fun (args : AdapterView.ItemClickEventArgs) ->
            let myView = args.View :?> TextView 
            Toast.MakeText(this.BaseContext, myView.Text , ToastLength.Long).Show()
            
            
The code is available in GitHub

https://github.com/vb2ae/FSharpAndroidList

