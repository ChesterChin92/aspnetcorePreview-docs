# Project initialization

From this part on, it's assumed that we have chose the following:
- Time tracker as the domain - see [previous part](03-choosing-a-domain.md)
- ASP.NET Core Web API application template as a base
- Visual Studio 2019 as the IDE of choice
- Git tools integrated in Visual Studio

In this part, we'll initialize our project, configure the git repository, connect it with GitHub and see how to use Postman to test our API. But first, we'll have a brief introduction to REST APIs.

## REST API introduction

This introduction is done in form of PowerPoint presentation. It explains what REST API is, the steps necessary to make production-ready API and how ASP.NET Core can help us with that. You can download the presentation [here](rest-api-introduction.pptx).

## Creating a project

Create a new ASP.NET Core Web Application project in Visual Studio 2019, name it *TimeTracker*, and finally select API as a template:

![New API project](images/vs-new-aspnetcore-api.png)

### Optional step

This step is optional, but it's a good practice to tidy up your source code repository. For git repositories, it's a convention to have `src` folder in your root to hold all source code. Let's modify our folder structure in order to do so. You'll need to close the Visual Studio in order to make the changes. This is how your folders should look like after the change:

![TimeTracker folder structure](images/timetracker-src-folder.png)

- `aspnetcore-workshop` - this is the root folder in my case, your root folder name might differ
    - `src` - folder containing all the projects, for now we have only one API project
        - `TimeTracker` - folder for TimeTracker API project
            - `TimeTracker.csproj` and other files and folders
- `TimeTracker.sln` - solution file

You can check the structure in this GitHub repository. There will be other folders next to `src`, like `test`, `doc`, etc.

Now that the folder structure is created, let's modify `TimeTracker.sln` file to point to a new location of `TimeTracker.csproj` file. Modify the line that looks like this:

    Project("{FAE04EC0-301F-11D3-BF4B-00C04F79EFBC}") = "TimeTracker", "TimeTracker\TimeTracker.csproj", "{6B239834-5A44-48A7-A80A-1DC9BA1B6A88}"

Into this (leave the same Guid values, just change the path to `.csproj` file):

    Project("{FAE04EC0-301F-11D3-BF4B-00C04F79EFBC}") = "TimeTracker", "src\TimeTracker\TimeTracker.csproj", "{6B239834-5A44-48A7-A80A-1DC9BA1B6A88}"

Open the solution file in Visual Studio to continue working on it.



## Running the application

By default, Visual Studio will configure your application to run under IIS Express web server, with a specific port. You can press `F5` or click on `▶️ IIS Express` button in the toolbar to run the server and browse your application.

Your browser might give you a warning about potential security risk. That's because HTTPS is used by default, and IIS Express is using self-signed certificate for local development. Browsers do not like self-signed certificates, hence the warning. You can ignore it and proceed (Accept the risk and continue).

API template comes with `WeatherForecastController` that serves as a sample for API. When you run the app, the browser will go to `https://localhost:port/weatherforecast` (where port is your port number) and return JSON with an array of weather forecast information for the next 5 days. This is what we expect, but browsers aren't really good when trying APIs, since we also need to have the ability to easily create `GET`, `POST`, `PUT` and `DELETE` methods, define parameters, etc. For that purpose, other tools should be used. Enters Postman.

## Using Postman

[Postman](https://www.getpostman.com/) is a tool for managing APIs. We can also use it to quick test if everything is working correctly with our API.

Run Postman and create a new GET request. Enter `https://localhost:port/weatherforecast` as URL and click *Send*. You should get HTTP status code 200 in response, with JSON payload.

![Postman first request](images/postman-first-request.png)

Postman allows you to create collections to organize your API calls. E.g. you could create a collection for your API, and have different request for each endpoint. Collections can be exported and shared. You can find the exported Postman collection for the sample API in the root of this repository.

We'll be using Postman throughout this workshop. To learn more about Postman, check it's excellent [documentation](https://learning.getpostman.com/).

-------

Next: [Domain models and database](05-domain-models-and-database.md)
