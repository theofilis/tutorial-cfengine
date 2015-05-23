* Create a new bundle
* Save the bundle as a .cf-file
* Copy the .cf file to /var/cfengine/masterfiles    
* Modify /var/cfengine/masterfiles/promises.cf to include your new bundle in the bundlesequence section
* Modify /var/cfengine/masterfiles/promises.cf to include your new .cf file in the inputs section