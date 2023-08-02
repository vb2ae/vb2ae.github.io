# Sitecore Serialization scindex error 

## I recieved the following error while trying to serialize sitecore items with the cli

dotnet sitecore ser push

     [core] Discovered 0 changes after evaluating 488 total items.

     Unhandled exception: System.Exception: Unhandled exception
     ---> System.InvalidOperationException: Error while reading subtree index file .scindex. Try deleting it; it will recreate itself.
     ---> System.InvalidOperationException: Line 394: YAML map value was not the valid GUID that was expected. Got "e786a623
     at Sitecore.DevEx.Serialization.Client.Datasources.Filesystem.Formatting.Yaml.YamlReader.GetExpectedGuid(String expectedKey, Func`2 mapFunction)
     at Sitecore.DevEx.Serialization.Client.Datasources.Filesystem.Query.FilesystemTreeIndex.YamlItemMetadata.ReadYamlAsync(YamlReader reader)

## To fix it I used a powershell script to delete the .scindex files

Run the powershell script from the solutions folder.  It loops through the folders in your solution and deletes any .scindex file.   After the script is run all the .scindex files will be recreated when you try and serialize again.


    $currentfolder = Get-Location
    Get-ChildItem -Path $currentfolder -File -Include *.scindex -Recurse | Remove-Item -Force -Verbose

