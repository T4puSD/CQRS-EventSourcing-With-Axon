# Event Sourcing with Axon and CQRS in Spring Boot

This is a demo project for learning event sourcing with axon framework and cqrs desing pattern.

## What is event Sourcing?
Event sourcing is a way to store events that occur in a business domain. For instance, In this demo project it is solving a banking domain problem. So, every events that occur in the domain needs to be stored for later review of a transaction or audit. Event sourcing helps in such conditions, it store every event in a formatted order for recalculation or re-evaluation. So perfectly naming all the event is crucial in this type of design.

## What is CQRS?
The full form of CQRS means Command Query Responsibility Segragation. It means that a business solution should have two separate service one should only change the state of the domain and other is only responsible to provide the view of the current state of the data. Commands are responsible for the state changes in a domain and Queries are responsible to provide view data to the end user.

## What is Axon?
Axon is a framework for solving such programming challenges. It helps programmer by leveraging all the configuration and abstract them. We as a spring boot developer just have to use annotation to solve the connection puzzle. To make it more easier axon now also provide their own axon server so that we can use that server as event store(Event store is the place/database where all the events reside).

## How this project is designed?
As this project is a command query responsibility segragation project. We have to separate all the command and events for the sake of it.

**It has 3 commands:**
1. CreateAccountCommand
2. CreditMoneyCommand
3. DebitMoneyCommand

**And 5 events:**
1. AccountActivatedEvent
2. AccountCreatedEvent
3. AccountHeldEvent
4. MoneyCreditedEvent
5. MoneyDebitedEvent

Every time a new command gets executed a new associated event gets generated for that command. For example when a new account gets created it trigger two events Account Created Event and Account Activated Event. Account Held event gets triggered if a user's account have negative balance. CreditMoneyCommand trigger the MoneyCreditedEvent and so forth.

## The Program Flow
When a new command is triggered through the controller it declare the command and event listener generate appropriate event for that command and it the the responsibility of the events to oprate on the domain model. For instance if CreditMoneyCommand is triggered then MoneyCreditEvent gets generated and operates on the entity model and increase the account balance. Axon framework will store this event into the axon server's event store.
