---
layout: post
title: An overview of yield return
categories: [dotnet, csharp]
tags: [yield, enumerable, generator]
---

While I was doing the online course [Python for the .NET developer](https://training.talkpython.fm/courses/details/python-for-dotnet-developers){:target="\_blank"} I've come accross the [yield return feature of C#](https://docs.microsoft.com/en-us/dotnet/csharp/language-reference/keywords/yield){:target="\_blank"}. I was suprised to learn it was in the language since V2.0 and I've never seen it used in any codebased I've worked in.

So what does is do ?
It's a contextual keyword used in a function which return an IEnumerable. It allows for _deferred execution_. It means that the evaluation of an expression is delayed until its realized value is actually required.
Take the following snippets which return an IEnumerable made of number of element in the Fibonacci sequence.

```cs
  public static void Main()
  {
    foreach (var i in Fibonacci(20))
    {
        Console.WriteLine(i);
    }
  }

  private static IEnumerable<int> Fibonacci(int count)
  {
    List<int> sequence = new List<int>();
    int current = 0;
    int next = 1;

    for (int i = 0; i < count; i++)
    {
        int temp = current;
        current = next;
        next = temp + next;

        sequence.Add(current);
    }

    return sequence;
  }
```

The function must calculate _all_ of the sequence before and then return the whole completed sequence.
Now let's see the same snippets refactored with yield return.

```cs
  public static void Main()
  {
    foreach (var i in Fibonacci().Take(20))
    {
      Console.WriteLine(i);
    }
  }

  private static IEnumerable<int> Fibonacci()
  {
    int current = 1, next = 1;

    while (true)
    {
      yield return current;
      next = current + (current = next);
    }
  }
```

You now see what seems to be an infinite loop with the `while true`! Well it's not one (kind of).
So as I've wrote the _yield return_ allows for _deferred execution_.

When the executed instruction reaches the yield return, the execution return to the caller of the function but, it keeps in memory where it was and picks up from there on the next iteration.

It's kind of hard to explain so let's see what it does looks like in debug:
![yield return debug next step]({{ site.baseurl }}/images/yield-return.gif "yield return exemple")

As you can see, only one element of the sequence is returned each time, as opposed to the first exemple where the whole sequence was return in one shot.
Why would you want to use this ? When you have a large sequence to iterate on, it's a better use case because it will use less memory and will be potentially faster.

Consider reading a file line by line as opposed to read the whole file in one big chunk to store it in memory. First you could run out of memory if it's a really big file! Second not using yield return can remove the gain to do a Parallel ForEach because the whole sequence must be computed before having a Parallel ForEach used on it.

Finally, in the course I've talked about in the beginning, I've learned that this is called a [generator](<https://en.wikipedia.org/wiki/Generator_(computer_programming)>){:target="\_blank"} in computer science. A lot of the most popular language has this feature in some kind of form or another!
