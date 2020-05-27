---
layout: post
title: An example of Strategy
categories: [dotnet, csharp, architecture]
tags: [design patterns]
---

This is my first foray in the world of using design patterns consciously.

The book _Design patterns : elements of reusable object-oriented software_ define The Strategy design pattern has:

> Define a family of algorithms, encapsulate each one, and make them interchangeable. Strategy lets the algorithm vary independently from clients that use it.

So what does it mean? In my demo app the [Dnd-Monster-Stats-Generator](https://github.com/AntoineLaroche/Dnd-Monster-Stats-Generator){:target="\_blank"} I've use the strategy pattern to encapsulate the implementation of the generation of he monster stats and the generation of the file output. Because these two functions varies depends on the options the user choose.
Heres the basic interface strategy for the monster stats generator:

<script src="https://gist-it.appspot.com/https://github.com/AntoineLaroche/Dnd-Monster-Stats-Generator/blob/master/DndMonsterStatsGenerator/Strategy/MonsterStatsGenerator/IMonsterStatsGeneratorStrategy.cs"></script>

The interface define a function which return a MonsterStats object and take a MonsterCreationOption object in parameter.

By doing that it allows the class which implements the interface strategy to determine at runtime which implementer it's going to use according to it's need. In the app case, the CR (Challenge Rating) is the determining factor the user choose which changes the method in which the monster stats are generated.

<sub>You probably don't know what a CR is if you're not familiar with dnd. Basically it's a number which qualifies the power of a monster, the higher the CR the higher the stats of the monster will be. The higher the stats, the more powerful a monster is.</sub>

For example, when the CR is between two and seven the formula to generate the monster stats is different from when is eight or higher. So heres the implementation of the monster generation formula when the CR is between two and seven:

<script src="https://gist-it.appspot.com/https://github.com/AntoineLaroche/Dnd-Monster-Stats-Generator/blob/master/DndMonsterStatsGenerator/Strategy/MonsterStatsGenerator/MonsterWithCRBetweenTwoAndSevenStatsGeneratorStrategy.cs"></script>

and heres the implementation of the monster stats generation formula when the CR is eight or higher.

<script src="https://gist-it.appspot.com/https://github.com/AntoineLaroche/Dnd-Monster-Stats-Generator/blob/master/DndMonsterStatsGenerator/Strategy/MonsterStatsGenerator/MonsterWithCREightOrHigherStatsGeneratorStrategy.cs"></script>

So at runtime, the app can use a variable of type IMonsterStatsGeneratorStrategy and just call the GenerateMonsterStats function. Also the app use a Factory to determine which strategy to use according to the CR. The Factory return the good implementation of the IMonsterStatsGeneratorStrategy according to the CR chosen by the user.

```cs
    public class MonsterStatsCreatorService : IMonsterStatsCreatorService
    {
        private readonly IMonsterStatsGeneratorStrategyFactory monsterStatsGeneratorStrategyFactory;

        public MonsterStatsCreatorService(IMonsterStatsGeneratorStrategyFactory monsterStatsGeneratorStrategyFactory)
        {
            this.monsterStatsGeneratorStrategyFactory = monsterStatsGeneratorStrategyFactory;
        }

        public MonsterStats CreateMonsterStats()
        {
            IMonsterStatsGeneratorStrategy monsterStatsGenerator = this.monsterStatsGeneratorStrategyFactory.Get(creationOption);
            return monsterStatsGenerator.GenerateMonsterStats(creationOption);
        }
    }
```

In conclusion, the strategy in the app helps with maintaining the separation between the different formulas to create monster stats. It's used with the file creator too, with the same principles, if the user want an xml or a json the strategy is there for them too.

The strategy could have been an abstract class with overridden function but I prefer to use composition over inheritance because it allows more flexibility. It also helps with respecting the Open/Close SOLID principle, because if one formula needs to change only that class will change and not the other formula and not the client.
