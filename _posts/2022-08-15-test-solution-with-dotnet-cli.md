---
layout: post
title: "Scripting the dotnet CLI for Rapid Test Setup"
date: 2022-08-15 15:56:42 -0600
---

From time to time, I need to create a small C# or F# solution to experiment with a code feature or a library function. Often, what I want to do is create a simple console application and a unit test project that references the console application. This isn’t hard to do in Visual Studio, but it feels like it takes too many steps.

Recently, I read a fantastic new book called Essential F#, by Ian Russel. (You can get [it here](https://leanpub.com/essential-fsharp)) In it, he showed that you could quickly create the setup I described above with the dotnet CLI. It was an idea so brilliantly simple that I’m jealous that I didn’t think of it. But I did take it a step further and created a bat file to further automate the process.

The commands in this script are taken directly from the book. The only modification I’ve made is to parameterize the solution name and the project name.

```
dotnet new sln -o %1
cd %1
mkdir src
dotnet new console -lang F# -o src/%2
dotnet sln add src/%2/%2.fsproj
mkdir tests
dotnet new xunit -lang F# -o tests/%2Tests
dotnet sln add tests/%2Tests/%2Tests.fsproj
cd tests/%2Tests
dotnet add reference ../../src/%2/%2.fsproj
dotnet add package FsUnit
dotnet add package FsUnit.XUnit
dotnet build
dotnet test
```

With this script, you could execute something like this command:

`CreateFSharpProject SampleSolution SampleProject`

This would create a new Solution named SampleSolution. It would contain two projects F#, SampleProject and SampleProjectTests. The test project already has a reference to the primary project and is ready to execute the tests with FsUnit.

I created a similar script file for C# and MSTest.
```
dotnet new sln -o %1
cd %1
mkdir src
dotnet new console -lang C# -o src/%2
dotnet sln add src/%2/%2.csproj
mkdir tests
dotnet new mstest -lang C# -o tests/%2Tests
dotnet sln add tests/%2Tests/%2Tests.csproj
cd tests/%2Tests
dotnet add reference ../../src/%2/%2.csproj
dotnet build
dotnet test
```
With these scripts, you can quickly create solutions with the unit test project already configured. That way, you can jump right into the code experiment you want to run.

You can take this concept and modify it to create whatever kind of project and unit test project you want. Hopefully, it is a simple little time saver for you.