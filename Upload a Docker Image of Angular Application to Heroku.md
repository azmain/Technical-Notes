
* Create a Heroku account.
* Install Heroku CLI on your local machine.
* Go to inside your project root directory.
* Login from terminal `heroku login`.
    >   you will then be prompt to enter your login credentials.
* Then login to Heroku container `heroku container:login`.
    >   you will be logged in to heroku container usring heroku credentials.
* This time I will push the image to an existing app created in Heroku by executing command `heroku container:push web -a existing_app_name`.
    >   It pushes the image to Heroku registry for existing_app_name.
* Release or Run the image on Heroku `heroku container:release web -a existing_app_name`.
    > Run the image. Voila our Angular application should be live!
* Open the app in the browser `heroku open`.
* In case you want to rename your app name. Run this command `heroku apps:rename newname --app oldname`.
 

### Resource
1. [R1](https://devcenter.heroku.com/articles/renaming-apps)




