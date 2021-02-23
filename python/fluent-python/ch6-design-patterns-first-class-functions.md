# Chapter 6: Design Patterns with First Class Functions
## What is the strategy pattern?
In the strategy pattern, a context object defers some computation to a strategy object that it holds. The strategy describes an interface that concrete strategies must implement. The motivation behind the strategy pattern is that the context object can select which concrete strategy object to use during runtime.

## What is the command pattern?
There are four key components involved in the command pattern: client, invoker, command and receiver.

Each concrete command implements a command interface and holds a receiver object. When the command is executed, it calls a method on the receiver object. A invoker object holds references to command objects and calls the execute method on them. The client decides what commands the invoker can execute and what receivers each command should hold.

## References
[1] https://en.wikipedia.org/wiki/Strategy_pattern

[2] https://en.wikipedia.org/wiki/Command_pattern