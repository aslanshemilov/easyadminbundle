# Custom Controllers

Now when we submit our form, obviously easy admin bundle's taken care of everything for us. Which sometimes can be a problem because sometimes we need to hook in, and maybe do some custom processing right before an entity is created or right before it's updated. For example, if you look at the user field, user entity it actually has an updated app field. Now of course, we could use a doctor and life cycle call back, or a doctor and events to accept that automatically whenever the user entity is created.

But I want to see if we can do it through easy admin bundle. What I mean is whenever we submit the user form for an update, I want to set that update at that field. There a couple of ways to do things like this depending on what you like in your situation. The easiest one is via the controller. Check this out. If you open up the easy admin controller and search for, protected function, there are a ton of methods that we can override beyond just the actions. Like create new entity, and pre persist entity, and pre update entity.

Meaning if we override pre update entity that methods going to be called every single time any entity is updated. There are a number of other interesting things that you can override. Cool, so very simple if we just override this inside of our controller then it's going to be called and we can update the updated app. Now let's go a step further, because if we do that this pre update entity is going to be called for every single entity in the system. But we really only want it called for the user entity.

Once again easy admin bundle has our back here. First inside the base controller I search for pre update entity in here, let's search our pre update. I'm actually going to see something up here called, this arrow execute dynamic method, pre updates, some weird code then entity. This is a really common thing that the admin bundle does. Whenever it calls almost any method inside of here, in fact you can even see, create edit form up here. It allows you to override that method for a specific entity by saying, for example, "Pre update user entity, or create user edit form."

If here we created a protected function, pre update user entity, it would call that only for our user entity and that gives you a lot of power. The way that I like to do it is to create a custom controller class for each individual entity. Check this out. Inside easy admin I'm going to copy admin controller and name it to user controller. Then I'm just going to empty out that function. Inside the [algo 00:03:23] code generates go to override methods, and we override pre update entity. Don't forget to update your class name to user controller.

We're going to configure things so that user controller is used only for the user entity. Which means that we can safely assume that this is going to be a user entity and we can make our code really simple here by saying, "Entity arrow set updated [app 00:03:47] new / date time." How does easy admin bundle know to use this controller only for the user entity? That happens inside of our configed dot [yml 00:04:04] down at the bottom where we have our user after a class I'll add controller. At bundle / controller / easy admin / user controller.

Just like that we have one controller just for doing things with our user entity. Let's try that out. Let's go find a user. If we look at user ID 20 right now, see it update now as [nul 00:04:37], so let's edit them. Makes them change, go back and updated app is set. Now that we know this is possible if you look at our admin controller it's actually a little sloppy because this change [public 00:05:03] status action, this is something that is only meant to work for the genus class. In fact, it's hard coded for the genus class right now.

Having an insight of admin controller is fine but it's only really needed for the genus controller. I'm going to also create a genus controller, so I'm going to copy and make a [chart 00:05:29] to genus controller. Before I fill in this logic I'm actually going to convert this admin controller to a base class for all of our admin controllers. We're not going to have anything in here for now but we will later. The genus controller, I'll rename the class and then we'll extend admin controller, and get rid of the old used statement. The user controller will do the same thing.

Extend the admin controller and we can get rid of some old used statements. Now the user controller just has the stuff that needs genus controller has just the stuff it needs, and if we need to over right something for all of our entities we can do it inside of admin controller. Of course, the last step is to remember to go into our configuration, all the way up on top, we'll set our controller to app bundle / controller / easy admin / genus controller. Now we're set up to do some really, really cool stuff.
