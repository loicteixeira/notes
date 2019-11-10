---
speakers:
- Justin Fagnani
topics:
- Web
videos:
- https://www.youtube.com/watch?v=x9YDQUJx2uw
---

# Building a Complex Application with Web Components and LitElement

Isolated components are easy but a full application is complex. It is a (much) bigger component with additionnal concerns: Routing, UI Singleton, Global State, Orchestration, etc.

## What are Web Components?

Web components are the native model of the web and encompass two things

- a custom (HTML) element
- a shadow DOM for encapsulation

For a web component to be available in the DOM:

-  Create a JavaScript class representing that element
  - It should extend the `HTMLElement` base class
  - It might react to some lifecycle events
- Register that class
- Import the file as `type="module"`

## What is LitElement?

LitElement:

- Is a collection of helpers to help create custom elements
- Is an implementation detail of your custom elements, not the defining part
- Uses declarative rendering
- Has reactive properties
- Is mostly asynchronous, the only exception being the render:
  - When a property is changed, it is queued
  - Then, rendering takes place
    - Better performances on multiple changes as it renders after all the changes instead of after each one
    - Easier to reson in templates since you don't have to reason about all the different cases of missing properties
    - If it was asynchronous, your app could be waiting seconds for the render to finish which would result in an unusable application.

## Patterns

### Routing

Use Data Driven Routing (with `page.js` for example) to decouple the routing from the URL.

The router consumes the URL, set the data accordingly and the component can decide for itself what to render.

It also allow for Event Driven Routing where raising an event would update the data which would then be picked up by the components.

It makes the data unidirectionnal.

### Code Loading

Avoid static imports, use dynamic import instead so JavaScript for a given route is only loaded when the user visit such resource.

### Async Tasks

Components can fire pending events for containers to catch (and handle) them.

This can be done by hand, but it would be better with a Cached Task helper:

- Do the  work asynchronously
- Fire LitElement `request_update` when done
- Fire a `pending` event
- Re-run if dependencies have changed

See the [Pending State Protocol](https://github.com/justinfagnani/pending-state-protocol) for more information

### Dependency Injection

How to get a component to access non-local data without having that data to be passed all the way down the three ?

It was usually done with a central Dependency Injection container which controls the constructor of a class to inject the required dependencies. But with Custom Elements, we can't control the constructor as it's called by the browser.

Instead, a component could request a dependency at startup via an event which any other component could provide.

This would be abstracted away with Requested and Provider mixins, however the component would still have to handle a missing resource in its rendering method (since the resource will come asynchronously).

Call to create a Dependency Resolution Protocol. Anyone?

### State Management

The motto: Data Down & Event Up. In other words, unidirectional data flow

However, it the project grows and this isn't viable anymore, it is still possible to hook with stores like Redux.
