# lv-launcher-nre

For context, this is meant as a kind of framework to organize the life cycel of the components within a given application. It's very similar to the given life cycle of various managed items within LabVIEW (Initialize > Write/Read > Shutdown). There are four recognized "states":

 * Start - this brings all components into memory nad in their default/un-configured states.
 * Initialize - this configures all in-memory components and "starts" their business logic.
 * Shutdown - this will stop all the business logic of all in-memory components and un-configure them. (hypothetically available for re-use)
 * Stop - This will take all components out of memory and clean up any references, it can be thought of as a de-constructor.
 
The short version, is that you should have a main launcher for every unique application you want to have within a project. IF you have two applications 1 and 2, they may have different components/modules that need to be started, initialized, shutdown and stopped.

## Integration

This architecture is HEAVILY influenced by MVVM (model view view model) ideas as well as the idea of "high cohesion but low coupling". There's an expectation that you have multiple individual modules which work independently and they are brought together by the main or some other interface that brings their functionality together to run some business logic.

**IF IT'S NOT ALREADY OBVIOUS** There's an assumption that your architeture has a minimum level of [Separation of Concerns](https://en.wikipedia.org/wiki/Separation_of_concerns) such that you can actualy take advantage of the launcher.

The event structure/while loop isn't necessary, but is meant to imitate a blocking interface that would be used in its place. Blocking is the easiest, but you could also use a handful of interfaces that navigate to each other as long as there's something that keeps the launcher main from continuing to the "shutdown" VI.