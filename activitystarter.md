# 活动启动器的用法

A component that can launch an activity using the `StartActivity` method.

Activities that can be launched include:

-   Starting another App Inventor for Android app. To do so, first find out the

     

    class

     

    of the other application by downloading the source code and using a file explorer or unzip utility to find a file named "youngandroidproject/project.properties". The first line of the file will start with "main=" and be followed by the class name; for example,

     

    ```
    main=com.gmail.Bitdiddle.Ben.HelloPurr.Screen1
    ```

    . (The first components indicate that it was created by Ben.Bitdiddle@gmail.com.) To make your

    ```
    ActivityStarter
    ```

     

    launch this application, set the following properties:

    -   `ActivityPackage` to the class name, dropping the last component (for example, `com.gmail.Bitdiddle.Ben.HelloPurr`)
    -   `ActivityClass` to the entire class name (for example, `com.gmail.Bitdiddle.Ben.HelloPurr.Screen1`)

-   Starting the camera application by setting the following properties:

    -   `Action: android.intent.action.MAIN`
    -   `ActivityPackage: com.android.camera`
    -   `ActivityClass: com.android.camera.Camera`

-   Performing web search. Assuming the term you want to search for is "vampire" (feel free to substitute your own choice), set the properties to:

-   Opening a browser to a specified web page. Assuming the page you want to go to is "www.facebook.com" (feel free to substitute your own choice), set the properties to:
