# Heroku

[Heroku](https://dashboard.heroku.com/) is an application hosting service that is rather easy to use.  Here are the steps to follow:

1. Create an account at [heroku.com](https://dashboard.heroku.com/).

2. Log into your Heroku account and create a new app.

3. Go to the Settings tab, find the Git URL for your app, and copy it to your clipboard.

![image1](https://github.com/mithatozturk/heroku/blob/master/settings_tab.png)

4. ```cd``` into your project's directory and add the repo whose url you just copied as a new remote.

    ```git remote add heroku https://git.heroku.com/stopcrocs.git```

When you want to deploy your app, all you have to do is push to this remote. But we're not ready to do that yet!

5. When your app runs on Heroku, certain information that you need will be made available to you as environment variables. You can access these through process.env. For example, the port on which your server should listen will be available as process.env.PORT. If you are listening on 8080 in your development environment, you should change your code in the following manner to work in production as well.

    ```app.listen(process.env.PORT || 8080);```

We will also have to do something similar with your database url. Let's first tell Heroku that we want to use Postgres.

6. Go to the Resources tab and add the Heroku Postgres add on. Make sure you choose the "Hobby Dev" plan, which is free.

![image2](https://github.com/mithatozturk/heroku/blob/master/resources_tab.png)

7. Download and install the Heroku CLI from [this page](https://devcenter.heroku.com/articles/getting-started-with-nodejs#set-up).

![image3](https://github.com/mithatozturk/heroku/blob/master/download_cli.png)

8. On the command line, log in with the Heroku CLI you installed.

    ```heroku login```
    
    You can now run the following command to get a psql prompt for your new db:

    ```heroku pg:psql```
    
    You can paste your ```CREATE TABLE``` commands here to set up your database.

9. The url for your database will be available to your code as process.env.DATABASE_URL. Update your code accordingly.

    ```var dbUrl = process.env.DATABASE_URL || 'postgres://spicedling:password@localhost:5432/petition';```

10. Commit your changes and push to deploy.

    ```git push heroku HEAD:master```

You will see a lot more going on in your terminal than you are used to. This is because immediately after receiving your push Heroku automatically deploys your app. If all goes well, you should be able to see your app running at your-app-name.herokuapp.com.

If all does not go well, you can gain insight into the problem by checking the logs.

![image4](https://github.com/mithatozturk/heroku/blob/master/logs.png)

**Note:** If you have configuration information in a file that you have listed in your ```.gitignore```, you can make it available to your Heroku app as environment variables. On the settings screen, click the "Reveal Config Vars" button and a UI for adding environment variables will appear. If, for example, you add a field named ```SESSION_SECRET```, you will be able to access the value of this field in your app with ```processs.env.SESSION_SECRET.```
    
    

