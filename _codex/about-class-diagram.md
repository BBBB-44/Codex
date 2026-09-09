What is a class diagram.

A class diagram is a type of structural diagram.

There are 2 main type of uml diagram : structural and behavioral.

Behavioral example : sequence or use case diagram.


A simple formula to remember
When designing a class, think:
Thing → Data → Actions → Responsibility → Relationships
For example:
Thing: Board ↓ Data: size, stones ↓ Actions: place stone, remove stones, check position ↓ Responsibility: manage the board ↓ Relationships: belongs to Game, contains Stones


Questions to ask yourself for each potential class
1. What is this thing?
Ask:
What object/concept am I representing?


2. What information does it need to remember?
Ask:
What data belongs specifically to this object?


3. What can this thing do?
Ask:
What actions naturally belong to this object?


4. Who should be responsible for this action?
This is one of the most useful questions:
Which class should be responsible for doing this?
For example, don't put:
Server.IsValidGoMove()

if the validation is really part of the game's rules.
Instead:
Game.IsValidMove()

The Game knows the rules, while the Server knows about networking.


5. Does this class have one clear responsibility?
Ask:
Can I describe what this class does in one short sentence?
Good:
Board manages the Go board.
Good:
Server manages network connections.
Bad:
Server manages connections, validates moves, calculates scores, displays the game, and saves files.


Is it actually a class?
Not every noun needs to become a class.
Ask:
Does this thing have its own data, behavior, or identity?
For example, Color might simply be an enum:


. Is this just a property of something else?
Ask:
Could this exist independently, or is it really just information belonging to another object?


