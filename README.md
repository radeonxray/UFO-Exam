# How _TypeScript_ and _Static typing_ can improve your _JavaScript_
> By _Christian Olsen_ & _Zaeem Rafique_


_Features such as _static typing_ can make it troublesome to switch from JavaScript to TypeScript. Static typing can be ignored or avoided, but doing so breaks some of the fundamentals of TypeScript in the process. While you will need to write a bit more code in TypeScript, you will end up with more readable, secure and less confusing code. Sticking to the rules of static typing will help you better maintain your project, even as it and your team grows larger._

# Intro to TypeScript
In this blog, we want to shed some light on _static typing_ in [TypeScript](http://www.typescriptlang.org/) (known as _TS_ from here on), how it affected the development of our [LSD-project](https://github.com/BingoBois), what we learned to do (and not do) and why you should consider using TypeScript next time you start a [JavaScript](https://www.javascript.com/)-project (known as _JS_ from here on).

_TS_ is a superset of _JS_ developed as an open-source project by Microsoft. This basically means that you are required to have some sort of knowledge and understanding of _JS_, since _TS_ and its new features are built on top of it.
Some of the features in _TS_ include built-in support for ES5, ES6 and future versions of ECMA-script, given the developers access to the latest _JS_ features. 

_TS_ also supports popular frameworks such as _React_, _React-Native_, _Vue_, _NodeJS_, _Angular_ and [more](https://www.typescriptlang.org/samples/index.html), and _TS_ is currently being used by companies such as _Bet365_, _SKY_, _UbiSoft_, _eBay_ and a lot of [more](https://www.typescriptlang.org/community/friends.html).

![Picture A ](https://cdncontribute.geeksforgeeks.org/wp-content/uploads/Untitled-102-300x216.png)

_Picture 1_

# The issue: When JavaScript goes from _dynamic_ to _static_
![Puzzle](/BlogAssignment/dynamictypingvsstatictyping-puzzle.png)

_Picture 2_

One of the big changes that _TS_ introduces to _JS_, is the switch from [_dynamic typing_ to _static typing_](https://medium.freecodecamp.org/why-use-static-types-in-javascript-part-1-8382da1e0adb).

The difference between these can be [explained](https://hackernoon.com/i-finally-understand-static-vs-dynamic-typing-and-you-will-too-ad0c2bd0acc7) as:
- _Dynamic typing_: _Type-checking_ at runtime
- _Static Typing_: _Type-checking_ at compile time

Due to this difference one of the benefits of _static typing_ is that [code optimization and performance will in general be better than _dynamic typing_](https://hackernoon.com/statically-typed-vs-dynamically-typed-languages-e4778e1ca55), since _static typing_ will not compile unless typing errors have been fixed, whereas _dynamic typing_ runs the risk of encountering type errors during runtime and crash the application. 
_Static typing_ makes _JS_ looking more like other languages such as [Java](https://www.java.com/en/), [C#](https://docs.microsoft.com/en-us/dotnet/csharp/) and many more.


# Evidence / Research 


## What does _static typing_ entail in TypeScript?

One of the great benefits of _TS_ is that it, thanks to the _[static typing](https://www.sitepoint.com/introduction-to-typescript/)_, detects a lot of potential errors and introduces _[type-checking](https://www.typescriptlang.org/docs/handbook/type-checking-javascript-files.html)_. If _TS_ detects an error at compile time, you will be notified immediately, and the code will not compile. To clarify the benefit of _static typing_, below is shown code examples showing the same function written in respectively _JS_ and _TS_.

![Picture C](/BlogAssignment/tsBasicJSEx.png) 

_Picture 3_



The above function expects a boolean value as parameter, but you can easily call the function with non-boolean parameters without getting any errors. E.g. you can pass the function a string as parameter and the code will still run without any problems. However, you will get an unexpected output from the function, and this may cause your entire program to respond in a different way than expected. By using _TS_[ type annotations](https://stackify.com/typescript-vs-javascript-migrate/), you can completely avoid encountering this problem.


_![Picture D](/BlogAssignment/tsBasicTSEx.png)_

_Picture 4_

On the above _TS_ code example, it's explicitly stated that the function is going to return a string and receive a boolean as parameter. If you still pass it with a non-boolean parameter, e.g. a string, you will immediately be shown an error message telling you that you are not allowed to pass the function a string as it expects a boolean. _TS_ has therefore made sure both that you have detected the error immediately and accurately showed where the error is.

Another quick example of _static typing_ is in the effect of _type-checking_, which means that variables (or return values in functions) must have their types defined, like string, number, Array etc.

![alt_text](/BlogAssignment/tsTypeAnnotation.png)


_Picture 5_



![alt_text](/BlogAssignment/tsTypeex.png)


_Picture 6: The same JS code as previously shown, but with errors due to being type-checked by TS._

## Why TypeScript?

[Stackoverflow](https://insights.stackoverflow.com/survey/2018) conducts a yearly survey asking their users various questions regarding their experience and thoughts about technologies. In 2018 over 100.000 developers from over 183 different countries completed the survey.


When asked about the technologies the developers [loved](https://insights.stackoverflow.com/survey/2018#most-loved-dreaded-and-wanted), 67.0 % said they loved _TS_ which placed it 4th out of 25, placing it only behind technologies as _Python_, _Kotlin_ and _Rust_, but it notably beating _JS_ which placed 7th with 61.9 %.

![SOF-MostLoved](/BlogAssignment/stackoverflow-MostLoved.png)

_Picture 7_

The fact that _TS_ beats _JS_ in the "Most Loved"-category would suggest that developers might be more happy working with _JS_ code when it's _TS_, which perhaps might be because of features and tools found in _TS_.  


## So how did _static typing_ affect our project?

Using _static typing_ meant that the team had to write and define more code (due to _type-checking_) than would probably be needed if the team had opted to use _dynamic typing_. 

As an example, below is a picture of an _interface_ (a definition for an _object_) with _typed_ variables.


![alt_text](/BlogAssignment/tsTypedInterface.png)


_Picture 8_

Note that the React.Component in the picture has "to know" what interfaces that are going to be used in the class and its state. This caused a lot confusion for most of the team members in the beginning, since they all of a sudden couldn't make simple array of objects like they had been used to in _JS_.

The tradeoff has been that the team has spent less time debugging for variables that have gone "bad" and perhaps mutated into other types than originally intended, while also avoiding un-instantiated variables. 
 
One of the simple _JS_ operations that slightly increased in complexity in _TS_, was when trying to get data from a simple input field.


![alt_text](/BlogAssignment/tsOnChange.png)


_Picture 9: A standard looking OnChange-function - same in TS as in JS_


When trying to extract the data in the handleCommentInput-function, the code now requires the developer to define the correct parameter _type_. This can sometimes result in spending a lot of time, which makes it even more important for the developers to know what tools and modules they are working with, so they can quickly narrow down the possibilities. 




![alt_text](/BlogAssignment/tsHandleCommentInput.png)


_Picture 10: Notice the type expected_

Another example of the amount of code required is shown in the picture below, where the method is required to define both the parameter _type_ and the return _type_. 


![alt_text](/BlogAssignment/tsHandleSubmit.png)


_Picture 11_


#


## The "Hacks" that starts disassembling TypeScript…

While _TS_ primarily uses _static typing_, types are still optional, meaning there are some "hacks" to avoid and ignore the rules set by _TS_, breaking the developer "contracts" and basically allow a type of _dynamic typing_.   


### any-keyword 

The [any type](https://www.typescriptlang.org/docs/handbook/basic-types.html) is a "wildcard" that re-introduces an element of _dynamic typing_ back into a _TS_-project, allowing the developer to mix and match _types_, as in _JS_.


![alt_text](/BlogAssignment/tsAnyKeyword.png)


_Picture 12_

One could argue that there is a small exception for choosing to use the "any"-keyword. Because many modules (in general) lack documentation for _TS_, it might not be possible to exactly define the right _type_ required for a function to return, hence why the use of the any-keyword may be the only possible solution.

### //@ts-ignore

![alt_text](/BlogAssignment/tsIgnoreActive.png)


_Picture 13_

Another way to avoid or in this case simply ignore an error thrown by _TS_, one can simply write "_[//@-ts-ignore](https://medium.com/@vitalyb/dont-let-typescript-slow-you-down-92d394ec8c9f)_" and then _TS_ will ignore the next line of code. 

But as with the exception for using the "_any_"-keyword, arguments for using "//_@ts-ignore_" can also be made, due to some libraries perhaps lacking proper _TS_ support and documentation.


The project was developed using technologies such as _React.js_ and _NodeJS_, special libraries (@types/) had to be downloaded in order to proper function with _TS_ as seen in the picture below, showing the projects [dependencies](https://nodejs.org/en/docs/meta/topics/dependencies/). These are also the libraries that can help avoid the need to use 
"//_@ts-ignore_"

![alt_text](/BlogAssignment/tsDependencies.png)

_Picture 14_

The effect of using these "backdoors" or "hacks" is that you start breaking the "contract" between you and your fellow developers. Functions may not work as intended and might not even take the correct parameters as the tooltip states, and you lose the code consistency of knowing that all your variables have and use the correct _type_.

For a large-scale project, using _TS_ correctly could therefore potentially greatly reduce the time and resources you might need to maintain the project. But you have to avoid the use of the "_any_"-keyword and "_//@ts-ignore_" as much as possible to achieve it.

# Alternatives

If one does not want to switch to _TS_, but still wants the benefits if _static typing_ in a _JS_-project, there are alternative ways to achieve this.

- The [_Form_](https://flow.org/) library developed by Facebook

![Flow](/BlogAssignment/flow.png)

_Picture 15_

- The open-source project [_Reason_](https://reasonml.github.io/)

![Reason](/BlogAssignment/ReasonLogo.png)

_Picture 16_

# Conclusion

On the positive side of _static typing_:

Yes, more work and time are required, but the benefits are a solid, stable and consistent code base and project structure, as well as great support for growing your code- and team-size.
_TS_ is quite popular right now, supports a lot of popular frameworks and offers great support for future _JS_ features and tools.

If you don't want to totally convert to _TS_ there are other options to switch your _JS_-project to _static typing_.

On the negative side of _static typing_: 
A lot of libraries still lack proper TS documentation and support, meaning the _"any-keyword"_ or _"//ts-ignore"_ can sometimes be the only option to continue development.

# Reflection

It took the team some time to get into the mindset of using static typing with _JS_, but based on our experience with using _TS_ during the development of our LSD-project, we would very likely use _static typing_ again, but perhaps by using a different approach, such as implementing _flow_. We sadly did not have enough time or pages to go into the bigger _“JavaScript vs. TypeScript”_ comparison or other beneficial features of _TS_, but we hope that this blog has given you enough of a taste for the benefits (and trappings) of _static typing_, so that you will give it a go yourself in your next _JS_-project, no matter if you implement it through using _TS_ or an alternative solution. If you have just a little experience with _JS_ and other languages such as _Java_ or _C#_, you should be up and running with _static typing_ pretty quickly.

# 


# Literature Resources: 



*   [Aux on TypeScript Pro's and con's](https://medium.com/@auxx/typescript-pros-and-cons-873529634099) 03/12-2018
*   [Why use TypeScript](https://itnext.io/why-use-typescript-good-and-bad-reasons-ccd807b292fb) 03/12-2018
*   [When should I use TypeScript](https://medium.freecodecamp.org/when-should-i-use-typescript-311cb5fe801b) 03/12-2018
*   [TypeScript and why one should use it](https://medium.com/tech-tajawal/typescript-why-should-one-use-it-a539faa92010) 03/12-2018
*   [Typescript vs. Javascript migration](https://stackify.com/typescript-vs-javascript-migrate/) 03/12-2018
*   [Its Time to give TypeScript another chance](https://medium.freecodecamp.org/its-time-to-give-typescript-another-chance-2caaf7fabe61) 03/12-2018
*   [Ionicframework and TypeScript](https://ionicframework.com/docs/developer-resources/typescript/) 03/12-2018
*   [Benefits of Migrating from JavaScript to TypeScript](https://blog.appdynamics.com/engineering/the-benefits-of-migrating-from-javascript-to-typescript/) 03/12-2018
*   [Learn TypeScript in 30 minutes](https://tutorialzine.com/2016/07/learn-typescript-in-30-minutes) 03/12-2018
*   [Site Point introduction to TypeScript](https://www.sitepoint.com/introduction-to-typescript/) 03/12-2018
*   [Why you might not want to use TypeScript](https://medium.jonasbandi.net/here-is-why-you-might-not-want-to-use-typescript-part-1-alternatives-ec1248bb6dc) 03/12-2018
*   [Why would you not use TypeScript](http://jonathancreamer.com/why-would-you-not-use-typescript/) 03/12-2018
*   [Stackoverflow Developer Survey](https://insights.stackoverflow.com/survey/2018#most-loved-dreaded-and-wanted) 03/12-2018
*   [Writing safer code with TypeScript strict null value](https://shinesolutions.com/2017/01/06/writing-safer-code-with-typescript-strict-null-checks-type-guards/) 03/12-2018
*   [The good, the bad and the ugly about TypeScript](https://blog.codeminer42.com/the-good-the-bad-and-the-ugly-of-typescript-58a3ff3e248) 09/12-2018
*   [Don't let TypeScript slow you down](https://medium.com/@vitalyb/dont-let-typescript-slow-you-down-92d394ec8c9f) 09/12-2018 
*   [TypeScript basics](https://www.typescriptlang.org/docs/handbook/basic-types.html) 09/12-2018
*   [TypeScripts class vs interface](https://medium.com/front-end-hacking/typescript-class-vs-interface-99c0ae1c2136) 09/12-2018
* [Finally understanding static- vs dynamic-typing](https://hackernoon.com/i-finally-understand-static-vs-dynamic-typing-and-you-will-too-ad0c2bd0acc7)12/12-2018
* [Statically typed vs Dynamically Typed](https://hackernoon.com/statically-typed-vs-dynamically-typed-languages-e4778e1ca55) 12/12-2018
* [Companies using TypeScript](https://www.typescriptlang.org/community/friends.html) 12/12-2018
* [Frameworks supported by TypeScript](https://www.typescriptlang.org/samples/index.html) 12/12-2018


Pictures:

1.  [Typescript And ES](https://cdncontribute.geeksforgeeks.org/wp-content/uploads/Untitled-102-300x216.png) 3/12-2018 
1.  [Static vs dynamic](https://i.redd.it/2uxj8u6yx9121.png) 12/12-2018
1.  Screenshot
1.  Screenshot
1.  Screenshot
1.  ScreenShot
1. [StackoverflowSurvey](https://insights.stackoverflow.com/survey/2018/#most-loved-dreaded-and-wanted) 12/12-2018
1.  Screenshot
1.  Screenshot
1.  Screenshot
1.  Screenshot
1.  Screenshot
1.  Screenshot
1.  Screenshot
1.  [Form](https://sdtimes.com/wp-content/uploads/2014/11/1118.sdt-flow.png) 12/12-2018
1.  [Reason](https://reasonml.github.io) 12/12-2018
