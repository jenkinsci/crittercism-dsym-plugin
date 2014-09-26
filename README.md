crittercism-dsym-plugin
=======================

This Jenkins CI plugin allows for a post build step that uploads dSYM files via Crittercism's API. The dSYM files are
used for symbolication of iOS binaries in Crittercism crash logs. As such, this plugin is only helpful for Mac OSX
hosts.

**USING THE CRITTERCISM-DSYM-PLUGIN:**

1. After installation, add a post-build step with the option 'Upload dSYM to Crittercism'.
2. The plugin requires three fields:
    a. **API Key** - Retrieve this from Crittercism's app dashboard, under 'Settings'.
    b. **App ID** - Also available from the Crittercism app 'Settings'.
    c. **dSYM zip** file - Path to the dSYM zip file to be uploaded. You may use environment variables. Ex: '${WORKSPACE}/build/MyApp-dSYM.zip'.

The plugin may encounter the following errors while uploading the dSYM file:

**Error 400**: There was a problem with the dSYM file.

**Error 404**: App was not found or the given tokens are incorrect.

**Note:** Depending on your configuration, the dSYM zip file generated in your build steps may be named something like
'MyApp-1.0-dSYM.zip', where 1.0 is your version number and may change with each build. To make things easier for the
post-build steps, you can rename your dSYM zip file to something static, such as 'MyApp-dsym.zip'. To accomplish this,
add a build step that executes shell commands, such as:

      mv ${WORKSPACE}/build/*dSYM.zip ${WORKSPACE}/build/MyApp-dSYM.zip


**BUILDING THE CRITTERCISM-DSYM-PLUGIN:**

1. Ensure you have maven 2 installed.
1. Check out the code with git.
2. In a console, cd to the checkout directory.
3. To build, run 'mvn package'.
4. To generate the *.hpi file, run 'mvn install'. The *.hpi file will be placed under the 'target' directory.

**EXTENDING THE CRITTERCISM-DSYM-PLUGIN:**

If you'd like to contribute changes to the plugin, feel free to contact me via GitHub or message me on Twitter @mmh02.

**REFERENCES:**

1. **Critter Docs iOS**: http://docs.crittercism.com/ios/ios.html#uploading-dsyms-via-the-command-line
