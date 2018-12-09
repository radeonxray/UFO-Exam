# What to watchout for when transitioning from Javascript to Typescript


# Abstract

* Features such as _static typing_ can make it troublesome to switch from JavaScript to TypeScript.

* Static typing can be ignored or avoided, but doing so breaks some of the fundamentals of TypeScript in the process.

* While you will need to write a bit more code in TypeScript, you will end up with more readable, secure and less confusing code.

* Sticking to the rules of static typing will help you better maintain your project, even as it and your team grow larger.


# The issue: When JavaScript goes from _dynamic_ to _static_

For our Large System Development project ["Hackernews-clone](https://github.com/BingoBois)", the development team tried to develop the project using the [TypeScript](http://www.typescriptlang.org/) programming language, in conjunction with other technologies such as React.js, NodeJS and more.

For those unfamiliar, TypeScript is a superset of [JavaScript](https://www.javascript.com/). This basically means that you are required to have some sort of knowledge and understanding of JavaScript, since TypeScript and its new features are built on top of it. 

![Picture A ](https://cdncontribute.geeksforgeeks.org/wp-content/uploads/Untitled-102-300x216.png)

_Picture 1_

But while changing to another programming language, even those that are build upon an existing one and one you might be very familiar with, there is always going to be a [learning curve](https://medium.com/quick-code/top-tutorials-to-learn-typescript-c08834892e69) and the development of this project was no exception. 

Because using TypeScript means that JavaScript changes from being _[dynamically-typed to statically-typed](https://medium.freecodecamp.org/why-use-static-types-in-javascript-part-1-8382da1e0adb)_, something seen in other programming languages like [Java](https://www.java.com/en/), [C#](https://docs.microsoft.com/en-us/dotnet/csharp/) and many more.

![Picture B](/BlogAssignment/futurerama.jpg)

_Picture 2_

So in this blog, we want to shed some light on _static typing_ in TypeScript, how it affected the development of our LSD-project, what we learned to do (and not do) and why you definitely should give it a try the next time you start a JavaScript project.


# 


# Evidence / Research 


## So what does _static typing_ entail in TypeScript?

One of the great benefits of TypeScript is that it, thanks to the _[static typing](https://www.sitepoint.com/introduction-to-typescript/)_, detects a lot of potential errors and introduces _[type-checking](https://www.typescriptlang.org/docs/handbook/type-checking-javascript-files.html)_. This means that TypeScript compiles and checks the code for errors even before you execute your program. If TypeScript then detects an error at compile time, you will be notified immediately and the code will not compile. To clarify the benefit of static typing, below is shown code examples showing the same function written in respectively JavaScript and TypeScript.

![Picture C](/BlogAssignment/tsBasicJSEx.png) 

_Picture 3: The above JavaScript code example demonstrates one of the biggest problems you may encounter by using plain JavaScript_



Although the above function expects a boolean value as parameter, you can easily call the function with non-boolean parameters without getting any errors. E.g. you can pass the function a string as parameter (as in the example above) and the code will still run without any problems. However, you will get an unexpected output from the function, and this may cause your entire program to respond in a different way than expected. By using TypeScript's[ type annotations](https://stackify.com/typescript-vs-javascript-migrate/) you can completely avoid encountering this problem.


_![Picture D](/BlogAssignment/tsBasicTSEx.png)_

_Picture 4_

On the above TypeScript code example, it's explicitly stated that the function is going to return a string and receive a boolean as parameter and you are therefore not allowed to pass the function non-boolean values. If you do so anyway, e.g. by passing the function a string (as shown in the example above), you will immediately be shown an error message telling you that you are not allowed to pass the function a string as it expects a boolean. TypeScript has therefore made sure both that you have detected the error immediately and accurately showed where the error is.

Another quick example of _static typing_, is in the effect of _type-checking_. This means that for example variables (or return values in functions as seen in the previous picture) has to have their types defined, like string, number, Array etc. This effectively creates a "contract" for the developers that needs to be uphold, if the project is to compile correctly.



![alt_text](/BlogAssignment/tsTypeAnnotation.png)


_Picture 5: The code above is a very simple example that shows how variables are mutable in JavaScript_



![alt_text](/BlogAssignment/tsTypeex.png)


_Picture 6: The same JavaScript code as previously shown, but with errors due to being type-checked by TypeScript._



One last feature that _static typing_ introduces is the concept of _[tree shaking](https://medium.com/@FloSloot/tree-shaking-lets-implement-it-8de1c29f49e9)_, which makes sure that the bundler only includes libraries or the parts of the libraries that are actually used.

However, the team did not get around to fully implement this feature in the project.

![alt_text](/BlogAssignment/treeshaking2jpg.jpg)


_Picture 7_




## So how did _static typing_ affect our project?

The team spent quite some time getting adjusted to the fact that we were writing JavaScript-code, but with some modern features and rules. Developers would often forget to specify the _type _of a variable, especially when creating _[interfaces](https://medium.com/front-end-hacking/typescript-class-vs-interface-99c0ae1c2136)_, thus making it impossible to compile the project. 

Using _static typing_ meant that the team had to write and define more code (thanks to _type-checking_) than would probably be needed if the team has opted to use _dynamic typing_. 

As an example, below is a picture of an _interface _(basically a definition for an _object_) with typed variables.


![alt_text](/BlogAssignment/tsTypedInterface.png)


_Picture 8_

Also note in the picture that the React.Component has "to know" what interfaces are going to be used in the class and its state. This caused a lot confusion for most of the team members in the beginning, since they all of a sudden couldn't make simple array of objects like they had been used to in JavaScript.

The tradeoff however, has been the fact that the team has spent less time debugging for variables that have gone "bad" and perhaps mutated into other types than originally intended, while also avoiding un-instantiated variables. 



While the project was developed using technologies such as React.js and NodeJS, special libraries (@types/) had to be downloaded in order to proper function with TypeScript as seen in the picture below.



![alt_text](/BlogAssignment/tsDependencies.png)


_Picture 9_ 

One of the simple JavaScript operations that suddenly slightly increased in complexity in TypeScript, was when trying to get data from a simple inputfield.


## 

![alt_text](/BlogAssignment/tsOnChange.png)


_Picture 10: A fairly standard looking OnChange-function in a JSX-element. Same in TypeScript as in JavaScript_


However, when trying to extract the data in the handleCommentInput-function, the code now requires the developer to define the correct parameter _type_. This can sometimes result in spending a good amount of time, which makes it even more important for the developers to know what tools and modules they are working with, so they can quickly narrow down the possibilities. 




![alt_text](/BlogAssignment/tsHandleCommentInput.png)


_Picture 11: Notice the type that is expected for the event-variable_

Another example of the amount of code required, is shown in the picture below, where the method is required to not only define the parameter _type_, but also the return _type_. 


![alt_text](/BlogAssignment/tsHandleSubmit.png)


_Picture 12_


## 


## The "Hacks" that starts disassembling TypeScript…

While TypeScript primarily uses _static typing_, types are still optional, meaning there are some "hacks" to avoid and ignore the rules set by TypeScript, breaking the developer "contracts" and basically allow a type of _dynamic typing_.   


### any-keyword 

The [any type](https://www.typescriptlang.org/docs/handbook/basic-types.html) is a "wildcard" that re-introduces an element of _dynamic typing_ back into a TypeScript project. It allows the developer to mix and match _types_, as seen in JavaScript and in picture E (to allow "any" interface to work in the class).


![alt_text](/BlogAssignment/tsAnyKeyword.png)


_Picture 13: The use of the "any" keyword in action._

One could argue however, that there is a small exception for choosing to use the "any"-keyword. Due to the fact that many modules (in general) lack documentation for TypeScript, it might not be possible to exactly define the right type required for a function to return, hence why the use of the any-keyword may be the only possible solution.

//@ts-ignore

![alt_text](/BlogAssignment/tsIgnoreActive.png)


_Picture 14_

Another way to avoid or in this case simply ignore an error thrown by TypeScript, one can simply write "_[//@-ts-ignore](https://medium.com/@vitalyb/dont-let-typescript-slow-you-down-92d394ec8c9f)_" and then TypeScript will ignore the following line of code. 

But just as with the exception for using the "_any_"-keyword, arguments for using the "//_@ts-ignore_" could also be made, due to some libraries perhaps lacking proper TypeScript support and documentation.

The effect of using these "backdoors" or "hacks", is that you start breaking the "contract" between you and your fellow developers. Functions may not work as intended and might not even take the correct parameters as the tooltip states, and you loss the code consistency of knowing that all your variables have and use the correct _type_.

 
For a large scale project, using TypeScript correctly could therefore potentially greatly reduce the time and resources you might have needed to maintain the project. But you have to avoid the use of the "_any_"-keyword and "_//@ts-ignore_" as much as possible to achieve it.


# Conclusion

While the team had some problems adjusting to TypeScript and _static typing_ in the beginning of the project, in the end, we became quite fond of developing using it. 


Once we got more comfortable working with typing standards we were familiar with from other programming languages, but now in a JavaScript-project, a lot of the initial complaints and headaches began to subside.

Yes, because of _type-checking_, it does take more work and code than just plain JavaScript, as well as the checks at compile time. But as we've hopefully shown throughout this blog, the benefits of minimizing mistakes, less time spent debugging and finding errors was a great tradeoff.

As seen in a couple of examples however, we admit that we did not follow the standards perfect during the project, since we've used the "_any_"-keyword and the "_//@ts-ignore_"-command. We hope that, as more and more modules roll out support for TypeScript, we will be able to go back and apply the correct use of TypeScript and _static typing_ in the instances where we cut corners in order for development to progress. 

It's important not to get tempted to only and always use such "hacking" features, since it defeats the purpose of _static typing_, and may hamper the future growth and development of your project.

[Aux](https://medium.com/@auxx/typescript-pros-and-cons-873529634099) summarized a similar point regarding _static typing_ and TypeScript:

"_Statically typed languages do minimise the amount of mistakes you make and improve code analysis so that all your tools like IDE can provide you hints, assistance and proper refactoring. _

_Yes, it forces you to type a bit more, and yes, types are optional in TS so you can easily shoot yourself in the foot, but I still find them very beneficial. _

_Especially for medium to large teams working on large projects which should be supported for many years._" 


# Reflection

The biggest challenge in transitioning from JavaScript to TypeScript, is your mindset. One could classify JavaScript as "_the wild west_", where pretty much everything is allowed at your own risk, and TypeScript is civilization coming to tame the wild land and establish some ground rules.

Based on our experience and if you want to create a new JavaScript-project that is able to lay down some coding standards and be suitable for a large team development, we can only highly recommend giving TypeScript a look. The learning curve can be tricky and the documentation for modules can sometimes be missing, but our team felt it was worth the hassle and extra hours in the end. Should TypeScript maintains its [popularity](https://insights.stackoverflow.com/survey/2018#most-loved-dreaded-and-wanted), the documentation will slowly and surely follow. 

We sadly didn't have time to go into all the topics and benefits related to TypeScript (and there are quite a few, such as [ECMAScript 5 + 6, transpiler to ECMAScript 3](https://blog.appdynamics.com/engineering/the-benefits-of-migrating-from-javascript-to-typescript/), ["Syntax sugar"](https://medium.com/@auxx/typescript-pros-and-cons-873529634099), browser compatibility and a lot of more), but if we did successfully catch your interest for learning more about TypeScript, we would highly recommend you to go learn about _interface_ and _[strict null checking](https://shinesolutions.com/2017/01/06/writing-safer-code-with-typescript-strict-null-checks-type-guards/)_, since both these topics can be used in conjunction with _static typing_ to great effect!

_![Picture P](/BlogAssignment/thewildwest.jpg)_

_Picture 15_

# 


# Literature Resources: 



*   [https://medium.com/@auxx/typescript-pros-and-cons-873529634099](https://medium.com/@auxx/typescript-pros-and-cons-873529634099) 03/12-2018
*   [https://itnext.io/why-use-typescript-good-and-bad-reasons-ccd807b292fb](https://itnext.io/why-use-typescript-good-and-bad-reasons-ccd807b292fb) 03/12-2018
*   [https://medium.freecodecamp.org/when-should-i-use-typescript-311cb5fe801b](https://medium.freecodecamp.org/when-should-i-use-typescript-311cb5fe801b) 03/12-2018
*   [https://medium.com/tech-tajawal/typescript-why-should-one-use-it-a539faa92010](https://medium.com/tech-tajawal/typescript-why-should-one-use-it-a539faa92010) 03/12-2018
*   [https://stackify.com/typescript-vs-javascript-migrate/](https://stackify.com/typescript-vs-javascript-migrate/) 03/12-2018
*   [https://medium.freecodecamp.org/its-time-to-give-typescript-another-chance-2caaf7fabe61](https://medium.freecodecamp.org/its-time-to-give-typescript-another-chance-2caaf7fabe61) 03/12-2018
*   [https://ionicframework.com/docs/developer-resources/typescript/](https://ionicframework.com/docs/developer-resources/typescript/) 03/12-2018
*   [https://blog.appdynamics.com/engineering/the-benefits-of-migrating-from-javascript-to-typescript/](https://blog.appdynamics.com/engineering/the-benefits-of-migrating-from-javascript-to-typescript/) 03/12-2018
*   [https://tutorialzine.com/2016/07/learn-typescript-in-30-minutes](https://tutorialzine.com/2016/07/learn-typescript-in-30-minutes) 03/12-2018
*   [https://stackify.com/typescript-vs-javascript-migrate/](https://stackify.com/typescript-vs-javascript-migrate/) 03/12-2018
*   [https://www.sitepoint.com/introduction-to-typescript/](https://www.sitepoint.com/introduction-to-typescript/) 03/12-2018
*   [https://medium.jonasbandi.net/here-is-why-you-might-not-want-to-use-typescript-part-1-alternatives-ec1248bb6dc](https://medium.jonasbandi.net/here-is-why-you-might-not-want-to-use-typescript-part-1-alternatives-ec1248bb6dc) 03/12-2018
*   [http://jonathancreamer.com/why-would-you-not-use-typescript/](http://jonathancreamer.com/why-would-you-not-use-typescript/) 03/12-2018
*   [https://insights.stackoverflow.com/survey/2018#most-loved-dreaded-and-wanted](https://insights.stackoverflow.com/survey/2018#most-loved-dreaded-and-wanted) 03/12-2018
*   [https://shinesolutions.com/2017/01/06/writing-safer-code-with-typescript-strict-null-checks-type-guards/](https://shinesolutions.com/2017/01/06/writing-safer-code-with-typescript-strict-null-checks-type-guards/) 03/12-2018
*   [https://blog.codeminer42.com/the-good-the-bad-and-the-ugly-of-typescript-58a3ff3e248](https://blog.codeminer42.com/the-good-the-bad-and-the-ugly-of-typescript-58a3ff3e248)
*   09/12-2018
*   [https://medium.com/@vitalyb/dont-let-typescript-slow-you-down-92d394ec8c9f](https://medium.com/@vitalyb/dont-let-typescript-slow-you-down-92d394ec8c9f)
*   09/12-2018 
*   [https://medium.com/@FloSloot/tree-shaking-lets-implement-it-8de1c29f49e9](https://medium.com/@FloSloot/tree-shaking-lets-implement-it-8de1c29f49e9)
*   09/12-2018
*   [https://www.typescriptlang.org/docs/handbook/basic-types.html](https://www.typescriptlang.org/docs/handbook/basic-types.html) 09/12-2018
*   [https://medium.com/front-end-hacking/typescript-class-vs-interface-99c0ae1c2136](https://medium.com/front-end-hacking/typescript-class-vs-interface-99c0ae1c2136) 09/12-2018



Pictures:

1.  [https://cdncontribute.geeksforgeeks.org/wp-content/uploads/Untitled-102-300x216.png](https://cdncontribute.geeksforgeeks.org/wp-content/uploads/Untitled-102-300x216.png) 3/12-2018 
1.  [https://memegenerator.net/instance/59547146/futurama-fry-not-sure-if-typescript-or-just-javascript](https://memegenerator.net/instance/59547146/futurama-fry-not-sure-if-typescript-or-just-javascript) 3/12-2018
1.  [https://stackify.com/typescript-vs-javascript<-migrate/](https://stackify.com/typescript-vs-javascript) 08-12-2018 19.43[ ](https://stackify.com/typescript-vs-javascript%3c-migrate/)
1.  [https://stackify.com/typescript-vs-javascript<-migrate/](https://stackify.com/typescript-vs-javascript) 08-12-2018 19.43[ ](https://stackify.com/typescript-vs-javascript%3c-migrate/)
1.  Screenshot
1.  ScreenShot
1.  [https://www.strava.com/clubs/266155](https://www.strava.com/clubs/266155) 09/12-2018
1.  Screenshot
1.  Screenshot
1.  Screenshot
1.  Screenshot
1.  Screenshot
1.  Screenshot
1.  Screenshot
1.  [https://www.thevintagenews.com/2017/12/16/wild-west-era/](https://www.thevintagenews.com/2017/12/16/wild-west-era/) 09/12-2018
