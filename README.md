# Heroku .NET Core Buildpack


This is the [Heroku buildpack](https://devcenter.heroku.com/articles/buildpacks) for [ASP.NET Core](https://docs.microsoft.com/en-us/aspnet/core/).

The Buildpack supports C# and F# projects. It searchs through the repository's folders to locate a `Startup.*` or `Program.*` file. If found, the `.csproj` or `.fsproj` in the containing folder will be used in the `dotnet publish <project>` command.

If repository contains **multiple** Web Applications (multiple `Startup.*` or `Program.*`), `PROJECT_FILE` and `PROJECT_NAME` environment variables allow to choose project for publishing.

## Usage

### .NET Core edge

```
heroku buildpacks:set https://github.com/CatenaTools/dotnetcore-buildpack
```

More info

- [Heroku Buildpack Registry](https://devcenter.heroku.com/articles/buildpack-registry)
- [Buildpack references](https://devcenter.heroku.com/articles/buildpacks#buildpack-references)

## Multiple Process Types
If you have multiple projects in a monorepo and wish to treat them as separate process types:
1. Build the projects simultaneously by setting the `PROJECT_FILE` config var to a solution file that references them.
2. Provide a custom `Procfile` in the directory of the `PROJECT_FILE` that enumerates the desired process types, for example:
```Procfile
web: cd heroku_output/; Catena__HttpConfig__Port=$PORT ./catena-tools-core --configEnv Heroku
```

## Example

[ASP.NET Core Demo App](https://github.com/jincod/AspNet5DemoApp)

## Source

This project is forked from https://github.com/jincod/dotnetcore-buildpack
