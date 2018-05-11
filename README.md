

# Gulp Env Modify

Add, edit, delete and read variables from a .env file. There is also functionality to help manage version named files.

### Installation
```
npm i gulp-env-modify --save
```
### Setup
```
const envmod = require('gulp-env-modify')
const env = envmod.getData()
console.log(env)
```
------

## Data functions

### Get File [*string*]

Get the .env file contents as a string

`envmod.getFile()`

*First parameter can be the path to your .env file relative to the gulpfile.js*

------

### Get Data [*object*]

Get the .env file content with all the variables and values passed into an object

`envmod.getData()`

*First parameter can be a direct request for a variable.*
*Second parameter can be the path to your .env file relative to the gulpfile.js*

------

## Get & Set functions

### Set Variable

Add a variable and value to the .env file. Variable will be created if it isn't found. It will be overwritten if it does exists.

`envmod.setVariable(variable, value)`

------

### Get Variable [*string*]

Get variable from .env file.

`envmod.getVariable(variable)`

------

## Versioning functions

There are a few options to manage variables that are suffixed with "_VERSION".  The purpose for this (and the reason I built this plugin), is to increment a variable each time a certain gulp task is called. Allowing me to generate unique file names for concatenated files. Ultimately this helps avoid browsers from caching old files whilst avoiding the use of ugly and unreliable url parameters.

### Get Version [*int*]

Get the version number of a variable

`envmod.getVersion(variable)`

------

### Update Version  [*int*]

Update the version number of a variable by incrementing the number by one.
| Parameter | Type | Description |
| - | - | - |
| name | string |  The name of the variable that prefixes the _VERSION variable  |
| force | int | By default this function will increment by one. However, you can update a variable to a specific number.|

`envmod.updateVersion(variable)`

------

### Get Version Name

To modify the filename for your gulp task, you will need to generate a dynamic name to match your latest version. This gives you that new filename.

| Parameter | Type | Description |
| - | - | - |
| file | string |  The original filename  |
| variable | string |  To find the latest version number, define the variable name to look for in the .env file. You do not need to include the suffix '_VERSION' |
| end | bool | Choose where the version number appears in the filename. This function looks for the **FIRST** full stop in the string, and prepends the version number to that. However  there may be cases where there are multiple full stops in a string. Define true to explicitly prepend the version number to the **LAST** full stop in the string. This is true by default. |

`modenv.getVersionName('main.min.js', 'js', true)`

This will look for the `JS_VERSION=12` in your .env file and return a string that looks like this

`main.v12.min.js`

If you set the `end` boolean to false, this would be returned instead:

`main.min.v12.js`

------

### Update Version Name

This essentially does the exact same thing as getVersionName, only it will increment the version in the .env file before returning the name filename.

------

### Delete Versions

Versioned files may start to get overwhelming and unnecessary. This lets you keep a set amount of versioned files.

| Parameter | Type | Description |
| - | - | - |
| directory | string |  Relative to your gulpfile.js, point to where your versioned files are stored.  |
| original | string | Pass the original filename so the comparison can match files after the version number has be verified |
| keep | int | Define how many versions of your versioned files you want to keep. By default this is set to 5.|

`envmod.deleteVersions('assets/js/', 'main.min.js', 3)`

------

### Credit
Couldn't have built this without [gulp-dotenv](https://github.com/pine/gulp-dotenv). Thank you.
