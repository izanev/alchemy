# Alchemy

Alchemy is a light-weight, event-driven, developer-friendly PHP framework.

#Introduction

Everyone knows that a framework is a set of libraries glued together to provide base scaffolding for project development and ongoing maintainance. Above all, we think that a framework has to provide security and structure to a developer. Too many times we have seen lack of real structure in frameworks. Innocent questions like "Where to put my code? Can I inject a service in the model?" give us clues of deeper-lying problems stemming from the fact that the creators themselves might not know "where the code should reside".

Therefore, we think it's very important for framework creators to use their product in real situations. Only then, they would close the creation process. Wouldn't a music composer play their own composition to gain insight as to how the composition sounds?

Yesterday, I found a WordPress® plug-in generator. Not only the generator worked like a charm, it also taught me so much things I couldn't have read in the WordPress® codex. For 5 minutes I had a boilerplate WordPress® plugin that was using the latest practices in plugin development. We need to have this principle applied to framework design as well: boilerplate project generation. Ready-made solutions for the common everyday problems. Need a project with admin panel, control panel and frontend - you have it ready-made. I would go as far as to say that code generation and boilerplate modules and projects are of higher priority that the framework itself.

It comes as a no surprise that being event-driven nowadays is a requirement. Components should not so much depend on one another. Events give us ways to decouple. However, if we make components event-driven, we are practically coupling the mechanism of event-handling to the components. What if a person wants to take a sole component from the framework? The ability to take a part of the framework and use it in different context is something important.

Last but not least, a framework should be light-weight. Such a framework would be easy to use and maintain and this results in the best productivity that a developer could have. Nowadays, people are used to the Route-Dispatcher-Controller-View strategy. The whole MVC idea comes from Smalltalk and PHP ain't no SmallTalk. PHP is about REST-fulness and always has been like that. Remember PHP 4? $_GET, $_POST, $_SESSION, header(), <?php echo ''; ?>, that's all! Honestly, how many times have you really used the Dispatcher Loop more than once in a request? Everytime, I have made a forward(), something feels really complex to me. 

We need to think of our Router not only as a way to simply handle the mapping of HTTP URI to controller and action. The Router must handle the whole request flow from its inception to the moment the View is rendered. This allows us to literally write magical formulas to control the flow of a request in our application. There is no "chain of command". Instead, we have several components piped in our Router that form the Request path in our application. Each Request has its own unique Context. More to the point, the incoming request needs to be treated with very high respect. Just the way you treat clients in your business. We are going to give names to our requests (e.g. CreateUserRequest) and each Request will also be an Event in our system (having a Context). 

The finite-state machine is another concept which we need to borrow. Dispatcher Loops were never supposed to be loops. The only reason that we make them loops is because someone said that "goto" is bad programming practice. Which is simply not true. Which is funny, because the whole internet works with a "goto" (think URL redirections and the stateless HTTP)? In other words, since we already have the Router which controls the Path of our Request, the Dispatcher Loop is uneccesary altogether. A component that, given a name of a controller, loads its class, is not a Dispatcher...it's an autoloader.

Another commonly disregarded feature of frameworks is Form generation. Mostly, because forms are also the domain of front-end developers. Most of the time, framework Form components sacrifice our ability to make it "look charming" just because we cannot figure out how to fit it all in with the decorators for example. First of all, we need to treat all components of HTTP with uttermost respect because that's our underlying technology. Radios, Checkbox Groups, Input Numbers, all form components are part of our Request. In fact, we can use Form Components to impose validations of our incoming requests. Forms are central in HTTP web pages and are treated in such way in our Alchemy.

What about Controllers?

Controllers, the way they are at the moment, are meaningless. The whole problem of "fat controllers" stems from the fact, that people subconcisouly try to use them in the way they are supposed to be used. Most of the time, when you come to the Controller, you start to execute Model logic, you mix it up with "View Logic" and it quickly becomes a mess. That's why frameworks introduced named parameters to actions (e.g. UsersController::edit($userID)). This is not a Controller, it's a Service and it's part of our Model already.

...Uhm, models?

Models are treated in very strange ways nowadays. Most of the time, a Model is a mix between an Object which represents an RDBMS table and its relationships, an Object which is supposed to handle Business Rules and impose Validations and on and on. In other words, the Model in most frameworks, is the place where we put things we do not know where else to put.

We are always talking about "Business Rules". Why are we not modelling them, people? Why are we not putting them into our codebase, into our namespaces? How come we always talk about things that we are not actually doing? Everything in our ubiqutious language (thank you, Eric Evans) should become more or less ingrained in our code production efforts.

To summarize:
- Event - central in the framework, in fact Exceptions are treated the same way as Events.
- Context - when an Event occurs we need to understand the Context in which it has occured. This gives us the possibility to have different Aspects of our "Alchemy".
- Component - base in framework, with ability to handle Events.
- Request - base in framework, the incoming request is what its all about.
- Input - the Request has one or more Inputs and they are your Form Components on which you can impose Validations.
- Router - sets up the Path of the Request in our Alchemy laboratory.
