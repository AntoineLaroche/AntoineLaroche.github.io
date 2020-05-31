---
layout: post
title: An example of Factory
categories: [dotnet, csharp, architecture]
tags: [design patterns]
---

In my [last post]({% post_url 2020-05-26-strategy-pattern %}) I've talked about the usage of the Strategy Design Pattern in my demo app, the [Dnd-Monster-Stats-Generator](https://github.com/AntoineLaroche/Dnd-Monster-Stats-Generator){:target="\_blank"}. I've mentioned how I use the Strategy in conjunction with a Factory.

It's now time to analyze the Factory Design Pattern. The book _Design patterns : elements of reusable object-oriented software_ define the factory method like this:

> Define an interface for creating an object, but let subclasses decide which class to instantiate. Factory Method lets a class defer instantiation to subclasses.

Considering this definition let's look at one of the factory in the app.

<script src="https://gist-it.appspot.com/https://github.com/AntoineLaroche/Dnd-Monster-Stats-Generator/blob/master/DndMonsterStatsGenerator/Factory/MonsterStatsGenerator/MonsterStatsGeneratorStrategyFactory.cs"></script>

The Factory method uses a pattern matching switch (from C# 8.0) to return the adequate Strategy according to the business logic. In this particular case, the Strategy is tied to the challenge rating.

The factory coupled with a strategy is used in the creation of the output file in the app too. The app support different file format so a factory is used to set the output file extension as you can see.

<script src="https://gist-it.appspot.com/https://github.com/AntoineLaroche/Dnd-Monster-Stats-Generator/blob/master/DndMonsterStatsGenerator/Factory/FileGenerator/FileGeneratorStrategyFactory.cs"></script>

It's the same principle, it's the file extension wanted by the user that's used to determine the strategy which implement the serialization to the file extension chosen by the user.

Here's how this factory is used:

<script src="https://gist-it.appspot.com/https://github.com/AntoineLaroche/Dnd-Monster-Stats-Generator/blob/master/DndMonsterStatsGenerator/Service/FileCreatorService.cs"></script>

It's injected in the file creator service. Doing this allows the file creator service class to abstract away the concern of the format chosen by the user and just validate if the file can be created and if it's valid to create it. In that way it respects the single responsibility principle.

It also respects the open/close principle. If a new file format is added or an existing file format is removed, the file creator service has no need to change, only the factory does.
