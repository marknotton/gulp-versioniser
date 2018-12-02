# Versioniser

![Made For NPM](https://img.shields.io/badge/Made%20for-NPM-orange.svg) ![Made For Gulp](https://img.shields.io/badge/Made%20for-Gulp-red.svg)

Cache bust filenames by automatically incrementing them with version numbers stored in your .env file.

## Installation
```
npm i @marknotton/versioniser --save-dev
```
```js
const versioniser = require('@marknotton/versioniser');
```
---
Versioner refers to your .env file when storing version numbers for filename manipulation. If your server doesn't support environmental variables in the form of a local .env file, then Versioniser is not for you.

There are a few options to manage variables that are suffixed with "_VERSION" y. The purpose for this (and the reason I built this plugin), is to increment a variable each time a certain gulp task is called. Allowing me to generate unique file names for concatenated files. Ultimately this helps avoid browsers from caching old files whilst avoiding the use of ugly and unreliable url parameters.

### Get Version [*int*]

Get the version number of a variable

`versioniser.getVersion(variable)`

------

### Update Version  [*int*]

Update the version number of a variable by incrementing the number by one.
| Parameter | Type | Description |
| - | - | - |
| name | string |  The name of the variable that prefixes the _VERSION variable  |
| force | int | By default this function will increment by one. However, you can update a variable to a specific number.|

`versioniser.updateVersion(variable)`

------

### Get Version Name

To modify the filename for your gulp task, you will need to generate a dynamic name to match your latest version. This gives you that new filename.

| Parameter | Type | Description |
| - | - | - |
| file | string |  The original filename  |
| variable | string |  To find the latest version number, define the variable name to look for in the .env file. You do not need to include the suffix '_VERSION' |
| end | bool | Choose where the version number appears in the filename. This function looks for the **FIRST** full stop in the string, and prepends the version number to that. However  there may be cases where there are multiple full stops in a string. Define true to explicitly prepend the version number to the **LAST** full stop in the string. This is true by default. |

`versioniser.getVersionName('main.min.js', 'js', true)`

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

`versioniser.deleteVersions('assets/js/', 'main.min.js', 3)`

------

### Credit
Couldn't have built this without [gulp-dotenv](https://github.com/pine/gulp-dotenv). Thank you!
