# python_design_playground


####Thoughts:
1. What is a Design Pattern?
2. Basic Principles of Design Patterns (2)
3.Behavioral Patterns
-List of some
-Focus on Facory Method Pattern (Dependency Injection and why that is good for testing)
4.Structural Pattern: Decorator Pattern
5. Behavioral Pattern : Chain of Responsibility
- Types

###### Resources
- https://www.toptal.com/python/python-design-patterns
- https://python-patterns.guide/


# Notes for Slides:

1. What is a Design Pattern?

-Everything starts with the Gang of Four:
<describe the Gang of Four Here>

Two Basic Principles:
1.a Program to an interface, not an implementation.

- Duck Typing

1.b Favor Object Composition Over Inheritance

- 

- Patterns are not invented, they are discovered.

2. Where are they baked into Python?

- Some design patterns are built into Python, so we use them even without knowing.


3. Where can I use thoughtful design in my code?

4. Behavioral Patterns

- Behavioral Patterns involve communications between objects, how objects interact and fulfil a given task.

11 total in Python: 
1. Chain of Responsibility
- This pattern maintains the "Single Responsibility Principle": Every piece of code must do one, and only one, thing
- 
2. Command
3. Interpreter
4. Iterator
- Iterators are built into Python
5. Mediator
6. Memento
7. Observer
8. State
9. Stategy
10. Template
11. Visitor


5. Creational Patterns
- Creational Patterns not as relevant to python because of the dynamic nature of the language. 
- There is no new operator in python.
- Creational Patterns provide a way to create objects while hiding the creation logic, rather than instantiating objects directly using a new operator.


5.a Singleton
- The Singleton pattern is used when we want to gurantee that only one instance of a given class exists during runtime.

Example of a Singleton for Logging:

```
class Logger(object):
    def __new__(cls, *args, **kwargs):
        if not hasattr(cls, '_logger'):
            cls._logger = super(Logger, cls
                    ).__new__(cls, *args, **kwargs)
        return cls._logger
```

- Not a very good example, really just use a module or create an instance somewhere at the top-level of your application, perhaps in the config file.

- Pass the instance of this object to every object that needs it. <Dependency Injection>
- dependency injection allows for felxible and esay unit-testing. 

Read: https://www.toptal.com/python/an-introduction-to-mocking-in-python

6. Structural Patterns

6.a Facade

- A Facade pattern stream lines an interface. Say you have object that has a lot of member variables that are other classes. And each of those member variable Classes can do many things individually. Well you can design the interface to just pull the most useful functions our all those available to the interface level. Facades can be used for interface simplification.

```
class Car(object):

    def __init__(self):
        self._tyres = [Tyre('front_left'),
                             Tyre('front_right'),
                             Tyre('rear_left'),
                             Tyre('rear_right'), ]
        self._tank = Tank(70)

    def tyres_pressure(self):
        return [tyre.pressure for tyre in self._tyres]

    def fuel_level(self):
        return self._tank.level
```

6.b Adapter <not clear on this>
- altering an interface
- bridge and proxy designs

6.c Decorator
- Already Integrated into the language
- the decorator pattern introduces additional functionality without inheritance

```
def execute(user, action):
    self.authenticate(user)
    self.authorize(user, action)
    return action()

```

- this is a bad function because the execute function does more than just execute something, so it does not follow the single responsibility principle.


This is more appropriate:
```
def execute(action):
    return action()
```


- Better version:

```
def autheticated_only(method):
    def decorated(*args, **kwargs):
        if check_authenticated(kwargs['user']):
            return method(*args, **kwargs )
        else:
            raise UnauthenticatedError
    return decorated


def authorized_only(method):
    def decorated(*args, **kwargs):
        if check_authorized(kwargs['user'], kwargs['action']):
            return method(*args, **kwargs)
        else:
            raise UnauthorizedError
    return decorated
    
@authorized_only
@authenticated_only
def execute(action, *args, **kwargs):
    return action()
```

- Look more into functools and decorators


- Opinions
Factory Design Pattern Not so Useful
