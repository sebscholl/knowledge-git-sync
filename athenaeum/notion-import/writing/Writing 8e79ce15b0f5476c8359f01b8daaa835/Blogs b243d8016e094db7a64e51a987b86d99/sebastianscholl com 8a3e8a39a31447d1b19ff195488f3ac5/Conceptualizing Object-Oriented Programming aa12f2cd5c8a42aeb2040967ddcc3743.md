# Conceptualizing Object-Oriented Programming

Created: August 23, 2021 5:48 PM
Location: New York City, United State of America
Original Publish Date: February 7, 2016
Tags: Education, Research

Last week I began Flatiron School. No, it's not to do with architecture. Campus occupies a large loft space at the southern most tip of Broadway Ave. It's convenient to pat the Wall St. bull along the commute. Once on campus I open my laptop, and code.

My journey as a developer started less than a year ago. What began as a self taught endeavor quickly transitioned to night school, and now, an immersive program. I've always considered myself a student whether enrolled in academia or not, employed or unemployed. Once again having the title is empowering, as there are no justifications to be made for why I'm dedicating my days to nothing other than honing a skill.

My curriculum expects me to write. This article will be the first of a series. The topics covered are mine to choose. My goal will be to relate technical concepts metaphorically. It's how I comprehend.

Now, onto the first topic - conceptualizing object-oriented programming.

![https://mynamessebastian.files.wordpress.com/2016/02/20150909_182721-1-01.jpeg](https://mynamessebastian.files.wordpress.com/2016/02/20150909_182721-1-01.jpeg)

Programming is logic. Logic used to reason inputs to outputs. The web is built on 1's and 0's as they represent true and false. The first computer programs simply accepted input data, processed it, and produced output data. This type of program was action oriented - as it had no concern for the input it was given. It always acted by the same logic.

Why was this a problem? Surely that is exactly what a program or machine should do. Act systematically to produce a consistent output. Early computer scientists tackled the challenge of how to write computer logic. However, as programs became more complex, the problem of *how do we define the data?* quickly arose.

Early programs were restricted by being singularly purposed. Since they didn't take any context from their inputs, they could only be designed to accept a single input. To best explain this, let's imagine we are writing a program called *Make Juice*. What does it do? It makes juice!

What are the steps involved in writing this program? Well, let's say we have an orange.

```
Make Juice
```

```
 Start Making Juice
```

1. `Is there an input? = True`
2. `Peel the input.`
3. `Cut it in half.`
4. `Squeeze one half above a glass bowl.`
5. `There is no more input to be squeezed? = False`
6. `Squeeze one half above a glass bowl.`
7. `There is no more input to be squeezed? = True`
8. `Pour into a cup all the liquid in the glass bowl.`

```
 Stop Making Juice

End
```

WAH-LAH! We have juice. Our *Make Juice* program is ready for action. Does it make juice? Yes it does. But what will it do if I give it an apple instead of an orange? Or god forbid, a carrot. *Exactly* what it was programed to do. And as you can imagine, for an apple, that wont do.

This type of challenge gave life to object-oriented programming. The idea that what's really important in programming are the inputs (objects) being handling rather than the methods used to handle them. It really wasn't that challenging to write out our logic and steps for the *Make Juice* program. However, how would we enable our program to properly make juice from different fruits and vegetables?

Well, we'd have to define an apple, an orange, and a carrot as objects- as well as every other fruit or vegetable that we'd like to juice. Also, we'd have to explain to our *Make Juice* program how to recognize which is which, as well as how to make juice from it. I'll be the first to say, THAT SOUNDS EXHAUSTING! But it's the only way, so I guess we have to start.

Good thing we already defined the steps for *Make Juice* to handle oranges. Next lets do grapefruits. Wait a minute, it's the same! What about lemons, limes, and tangerines? All the same. The reason behind this is no mystery. These fruits all come from the citrus family, meaning that they are *classified* as citrus fruits. This is big news for us and our *Make Juice* program, because now instead of writing out how to handle every single fruit, we can simply write out how to handle a fruit *class*.

Now, let's get back to our *Make Juice* program. And instead of programming it to handle oranges, we are going to program it to handle all citrus fruits as well pome fruits (e.g., apple and pear) - lets write some pseudo code.

```
Make Juice
```

```
  class Citrus
    Start Making Juice
      //Citrus juice instructions
    Stop Making Juice
  end Citrus
```

```
  class Pome
    Start Making Juice
      //Pome juice instructions
    Stop Making Juice
  end Pome

End
```

Look at how our program changed. It is no longer oriented around actions and logic, but instead classes. And what are those classes defined by? Data and inputs. Simply put, it is now object-oriented. In doing so, we've been able to both define our inputs within classes, and within that class provide the instructions needed for how such inputs should be handled. But how does our program know an apple is classified as a pome fruit and an orange citrus?

That process is known as data modeling, and it is a topic to be covered on its own. However, it doesn't really matter at this point. Why? Because if we give our *Make Juice* program an input it cannot run unless that input gets defined within a class! It is completely dependent on classifying the object it's given to access the instructions to handle that object.

So, in conclusion, when we first wrote *Make Juice*, the program was solely oriented around actions and logic, taking no context from inputs. By defining our inputs into *classes*, we were able to re-structure *Make Juice* to be oriented around the input. Even though *Make Juice* still does exactly what it's supposed to do (...make juice), we've now structured it to be object-oriented, enabling higher levels of complexity to its capabilities.

![https://mynamessebastian.files.wordpress.com/2016/02/20151017_171055-01.jpeg](https://mynamessebastian.files.wordpress.com/2016/02/20151017_171055-01.jpeg)