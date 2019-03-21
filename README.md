# run-core
A starter kit for your next web application. Boilerplate for ASP.NET Core reference application with Entity Framework Core, demonstrating a layered application architecture with DDD best practices. 

You can check full documentation and step by step development of 100+ page eBook PDF from here - http://www.aspnetrun.com/Book

ASP.NET Run is a general purpose starter kit application specially designed for new modern web applications. It uses already familiar tools and implements best practices around them to provide you a SOLID development experience.
This repository focused on traditional Web Application Development with a single deployment.

The goal for this boilerplate is to demonstrate some of the principles and patterns described in the [eBook](http://www.aspnetrun.com/Book). Also there is a sample project which is implemented this repository and build sample of eCommerce reference application, you can check this repo in this location : [run-core-sample](https://github.com/aspnetrun/run-core-sample)

ASP.NET Run works with the latest ASP.NET Core & EF Core.

## Getting Started

Clone or download repository. AspnetRun.Web should be the start-up project. Directly run this project on Visual Studio or use dotnet run command from terminal. You will see index page of project, you can navigate product and category pages and you can perform crud operations on your browser.

After cloning or downloading the sample you should be able to run it using an In Memory database immediately.
If you wish to use the project with a persistent database, you will need to run its Entity Framework Core migrations before you will be able to run the app, and update the ConfigureDatabases method in Startup.cs (see below).

```
public void ConfigureDatabases(IServiceCollection services)
{
    // use in-memory database
    services.AddDbContext<AspnetRunContext>(c =>
        c.UseInMemoryDatabase("AspnetRunConnection")
        .UseQueryTrackingBehavior(QueryTrackingBehavior.NoTracking));

    //// use real database
    //services.AddDbContext<AspnetRunContext>(c =>
    //    c.UseSqlServer(Configuration.GetConnectionString("AspnetRunConnection"))
    //    .UseQueryTrackingBehavior(QueryTrackingBehavior.NoTracking));
}
```

1. Ensure your connection strings in appsettings.json point to a local SQL Server instance.

2. Open a command prompt in the Web folder and execute the following commands:

```
dotnet restore
dotnet ef database update -c AspnetRunContext -p ../AspnetRun.Infrastructure/AspnetRun.Infrastructure.csproj -s AspnetRun.Web.csproj
```
These commands will create aspnetrun database which include Product and Category table. You can see from AspnetRunContext.cs.
1. Run the application.
The first time you run the application, it will seed aspnetrun database with a few data such that you should see products and categories.

These instructions will get you a copy of the project up and running on your local machine for development and testing purposes. See deployment for notes on how to deploy the project on a live system.

Don't Repeat Yourself! ASP.NET Run designed common software development tasks by convention. You focus on your business code!

```
public async Task<ProductDto> Create(ProductDto entityDto)
{
    await ValidateProductIfExist(entityDto);

    var mappedEntity = ObjectMapper.Mapper.Map<Product>(entityDto);
    if (mappedEntity == null)
        throw new ApplicationException($"Entity could not be mapped.");

    var newEntity = await _productRepository.AddAsync(mappedEntity);
    _logger.LogInformation($"Entity successfully added - AspnetRunAppService");

    var newMappedEntity = ObjectMapper.Mapper.Map<ProductDto>(newEntity);
    return newMappedEntity;
}
```

### Layered Architecture

AspnetRun provides a layered architectural model based on Domain Driven Design and provides a SOLID model for your application.


### Prerequisites

What things you need to install the software and how to install them

```
Give examples
```

### Usage

You can use this library using DotnetCrawler class with builder pattern in your console applications;

### Installing

A step by step series of examples that tell you how to get a development env running

Say what the step will be

```
Give the example
```

And repeat

```
until finished
```

End with an example of getting some data out of the system or using it for a little demo

## Running the tests

Explain how to run the automated tests for this system

### Break down into end to end tests

Explain what these tests test and why

```
Give an example
```

### And coding style tests

Explain what these tests test and why

```
Give an example
```

## Deployment

Add additional notes about how to deploy this on a live system

## Built With

* [Dropwizard](http://www.dropwizard.io/1.0.2/docs/) - The web framework used
* [Maven](https://maven.apache.org/) - Dependency Management
* [ROME](https://rometools.github.io/rome/) - Used to generate RSS Feeds

Development environments;

* Visual Studio 2017
* .Net Core 2.2 or later
* EF Core 2.2 or later

## Contributing

Please read [CONTRIBUTING.md](https://gist.github.com/PurpleBooth/b24679402957c63ec426) for details on our code of conduct, and the process for submitting pull requests to us.

## Versioning

We use [SemVer](http://semver.org/) for versioning. For the versions available, see the [tags on this repository](https://github.com/your/project/tags). 

## Next Releases

This program only imported EF.Core and using default downloader-processor-pipeline classes. And this program only solve spesific problem of customer requirements. So it will evolve a product and extent with new features as listed below;

* Extend with different database providers. 
* Extend for different downloader-processor-pipeline implementations which requested with different aproaches.
* Use with hangfire, quartz schedular frameworks in order to schedule and use async functions.

### Implemented Projects

You can check real-world example of run-core web application. In this repository you will find full implementation of e-commerce real-world example. [run-core-sample]

## Authors

* **Mehmet Ozkaya** - *Initial work* - [mehmetozkaya](https://github.com/mehmetozkaya)

See also the list of [contributors](https://github.com/aspnetrun/run-core/contributors) who participated in this project.

## License

This project is licensed under the MIT License - see the [LICENSE.md](LICENSE.md) file for details

## Acknowledgments

* Hat tip to anyone whose code was used
* Inspiration
* etc
