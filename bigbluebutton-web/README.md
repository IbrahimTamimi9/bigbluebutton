# BigBlueButton Web Grails 3 Deployment Procedure

Upgrade Gradle and Grails

```
# Install SDKMan if you don't have it yet.

curl -s "https://get.sdkman.io" | bash

# Install Gradle
sdk install gradle 5.1.1

# Install Grails
sdk install grails 3.3.9
```

To run the application from its source code : `grails prod run-app`

To run the application on a different port use : `grails -port=8989 prod run-app`

To run unit tests: `grails test-app --stacktrace`

To package the application for production:

1. Compile the application and package it use `grails assemble`
2. You now have the file `build/libs/bigbluebutton-0.10.0.war`
3. Create a new directory `mkdir exploded`
4. Navigate to that directory `cd exploded`
5. Extract the war content `jar -xvf ../build/libs/bigbluebutton-0.10.0.war`
6. Copy run script into exploded dir `cp ../run-prod.sh .`
7. Package the content of the new directory in a debian package then add service configuration. Install into `/usr/share/bbb-web`.
8. Create a systemd service file that runs `run-prod.sh`. App will be listening on port 8080
9. To do custom config, edit `/usr/share/bbb-web/WEB-INF/classes/bigbluebutton.properties`
Don't forget to use full directories path and replace the dot before the org with the full path to the exploded war.
