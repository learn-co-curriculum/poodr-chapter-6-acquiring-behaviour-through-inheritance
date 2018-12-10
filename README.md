# POODR - Chapter 6: Acquiring Behaviour through Inheritance

This chapter covers 'how to write inheritable code'

## 6.1 Understanding Classic Inheritence

"Inheritance is, at its core, a mechanism for automatic message delegation." - pg 105

## 6.2 Recognizing Where to use Inheritence

Problems with combinig styles into one class
- Code smell, if/else logic in `spares` checking on `:style`
  - Are all if/else blocks to be considered code smells?
    - 'Last option is the defualt' is damgerous
  - "This code contains an if statement that checks an attribute that holds the category of self to determine what message to send to self." - pg 111
- You don't know if you can send `tape_color` or `rear_chock` to any given instance

Finding the embedded types
- **Watch out for switching on things like `style`, `type`, `category`**
  - Where are some places you can think of in Ironboard where we might be doing this?

If an object does not know a method, its checks it's parent class and the process repeats until it gets to the top `Object`

"The fact that unknown messages get delegated up the superclass hierarchy implies that subclasses are everything their superclasses are, plus more." - pg 113

## 6.3 Missaplying Inheritence

Adding subclasses without perhaps first refactoring the parent class can be problematic. You need to make sure that the parent class only contains the things that _should_ be shared. 

## 6.4 Finding Abstraction

For inheritance to work, two things must always be true: (pg 117)
  - First, the objects that you are modeling must truly have a generalization–specialization relationship.
  - Second, you must use the correct coding techniques.

The parent class should be abstract such that you are not creating new instances of that class itslef (you don't create a new `Bicycle`, only a new `MountainBike` or `RoadBike`)

It can be beneficial to put off the creation of an abstract class until there are more examples (3+) so you can know more about the abstraction. 

"push-everything-down-and-then-pull-some-things-up" strategy:
- Take all the code from the would be parent class and put it into the specific class (`Bicycle` -> `RoadBike`) 
- Create the new subclass (`MountainBike`) and add the specifics you need. 
- Create the empty parent class for them to both inherit from `Bicycle`
- Test the new subclass `MountainBike` and promote the methods you need from `RoadBike` into `Bicycle`

> This method looks like one of the many things that feels like it's going to be more work to do 'the slow way', but seems to end up producing better code. 

This is a great strategy because it ensures that we don't accidentaly leave any concreteness in the superclass. Any failures of bringing an abstraction back up into the superclass is immediatley visible when using the new subclass. 

Pushing the concrete bits _down_ one at a time runs a much higher risk of leaving concrete code in the abstract class and subclass beging to violate rules of inheritence which can be harder to spot and become much harder to deal with. "Inexperienced programmers do not understand and cannot fix a faulty hierarchy; when asked to use one they will embed knowledge of its quirks into their own code, often by explicitly checking the classes of objects." - pg 123

The template method - Allows the superclass to specify some defaults while the sublcass can override with specificity. 

Superclasses may require methods of their subclasses that they themselves have not implemented. If you're going to do this, you should at least define a method on the superclass that raises an error to clearly alert the developer.

## 6.5 Managing Coupling Between Superclasses

"It makes sense that subclasses know the specializations they contribute (they are obviously the only classes who can know them), but forcing a subclass to know how to interact with its abstract superclass causes many problems." - pg 134

Hook messages make it more obvious what a subclasses needs to do and can be a better alternative to useing `super`. It keeps the subclass from having to know too much about how the parent class is implemented, though you do now need to know what hooks to use. 

## 6.6 Summary

"The best way to create an abstract superclass is by pushing code up from con- crete subclasses. Identifying the correct abstraction is easiest if you have access to at least three existing concrete classes." - pg 139
<p class='util--hide'>View <a href='https://learn.co/lessons/poodr-chapter-6-acquiring-behaviour-through-inheritance'>POODR Chapter 6: Acquiring Behaviour through Inheritance</a> on Learn.co and start learning to code for free.</p>
