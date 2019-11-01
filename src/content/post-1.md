---
title: "Back to R & R̶D(evelpoment)"
date: "2019-10-31"
draft: false
path: "/blog/back-to-r-and-d"
---

After spending several years in corporate management I found that with each passing month there was less and less time available for the two activities I love the most: making music and writing code. Time for a change!

With so many shiny new things to learn on the development front it has been hard to know where to begin. I looked at many of the latest and greatest frameworks and APIs and decide that I'd focus on working GraphQL and React hooks into my set list.

I also decided to make time for music and have made some commitments with some long time friends and former band mates but that will be another post :)

## GraphQL

Lots of buzz about GraphQL these days and rightfully so. After years of faithful service REST APIs have become increasingly clunky to leverage for getting at the data you really want. But what is GraphQL... exactly?

#### Getting the data you need

From the graphql.org website: "GraphQL is a query language for APIs and a runtime for fulfilling those queries with your existing data. GraphQL provides a complete and understandable description of the data in your API, gives clients the power to ask for exactly what they need and nothing more, makes it easier to evolve APIs over time, and enables powerful developer tools."

Ok. Not the clearest explanation. Let's have another go.

In simpler terms: GraphQL sends a query to a server as a string. The server interprets the string and returns JSON to the client. What makes GraphQL queries very different from REST API calls is the fact that a GraphQL query describes the 'shape' of returned data and the integrity of relationships are preserved in the returned JSON as you can see in the following image:

![image-20191031150520828](/Users/robinleboe/Library/Application Support/typora-user-images/image-20191031150520828.png)

#### Typing and Introspection

Because GraphQL is strongly [typed](https://graphql.org/learn/schema/) it can provide [introspection](https://graphql.org/learn/introspection/), in other words you can ask for the types of data types available for queries. Not only is this a great way to understand the data store you're working with it also means that descriptive error messages can be displayed before executing a query.

#### Protocol not data storage

It's important to point out that GraphQL is a protocol access your data not a way to store it. One of the things that makes GraphQL so incredibly useful is the fact that it leverages your existing code and storage. Using an abstraction layer like [Prisma](https://www.prisma.io/docs/1.4/reference/introduction/what-is-prisma-apohpae9ju) your existing databases can be queried using GraphQL complete with CRUD and realtime capabilities. As the Prisma docs explain, "It is the glue between your database and GraphQL server."

One stack that I've been working with consists of [React](https://reactjs.org), [Apollo](https://www.apollographql.com) on the client side and [GraphQL Yoga](https://github.com/prisma-labs/graphql-yoga) (Express GraphQL server) and [Prisma](https://www.prisma.io/docs/1.4/reference/introduction/what-is-prisma-apohpae9ju) for data abstracction on the server side. This covers everything you need and it's pretty easy to connect the new GraphQL approach to familiar tools. 

For those who are interested in getting their hands dirty [Wes Bos](https://wesbos.com/) has a great course called [Advanced React](https://advancedreact.com/). I have no affiliation but it's areally solid introduction to how all of the moving parts fit together in a GraphQL based stack.

## React Hooks

Since being introduced to the world about a year ago at the world at React Conf 2018, React Hooks have become wildly popular and have been rapidly trasforming the way developers build their applications. Since Hooks can be used alongside your existing code you can start using them right away and take migration at your own (or your client's) pace.

#### A sad state of affairs: HOCs, Lifecycle methods, converting to Classes

- In React apps logic has traditionally been shared using Higher Order Components and render props. Although using HOCs addressed the problem of sharing logic between components this approach added a layer of confusion, making code disjointed and harder to follow.

- Another thorny issue historically faced by React developers is the necessity of splitting logic across React's life-cycle methods: `componentDidMount` ,`componentDidUpdate`, and `componentWillUnmount`. Using React Hooks it is possible to keep logic together, making apps easier to read and debug. It also makes cleaning up after side effects easier and goes along way toward avoiding nasty memory leaks. With Hooks the need for `this` and  binding callbacks when dealing with state are also eliminated.

- Lastly but nor leastly, in past versions of React it was necessary to convert so-called stateless components (now generally referred to as functional components) to class components to gain access to state and life-cycle methods. 

#### React Hooks to the rescue!

With Hooks class components containing state can easily be converted to functional components using a few React Hook APIs: `useState`, `useEffect` and `useContext`. Life-cycle logic can be contained within a `useEffect` hook and can be reused multiple times within a component and shared across other components in an application. You can [create custom Hooks](https://reactjs.org/docs/hooks-overview.html#building-your-own-hooks) as well. 

Hooks do have a few limitations: they need to be used at the top level of functional components and they cannot be called inside loops, conditions, or nested functions. Also you can only call Hooks from React components.

Here's an example of a simple `useState` Hook from the reacts.org website:

```javascript
import React, { useState } from 'react';

function Example() {
  // Declare a new state variable, which we'll call "count"
  const [count, setCount] = useState(0); // destructuring assignment, initial state set to 0

  return (
    <div>
      <p>You clicked {count} times</p>
      <button onClick={() => setCount(count + 1)}>
        Click me
      </button>
    </div>
  );
}
```

As you can see in the above example, the `useState` Hook is leveraged inside a function component to add local state. React preserves state between renders, eliminating the need to convert the component to a class to track state.

Two `const` variables (oxymoron?) `count` and `setCount` are declared courtesy of ES 6 restructuring; one holding the current value and one holding the function to update it. As described on the [React site](https://reactjs.org/docs/hooks-overview.html#building-your-own-hooks), the only argument supplied to `useState` in this example is used for the purpose of setting the initial state i.e. `useState(0)`. The 0 indicates that the counter should increment starting from zero. 

Since Facebook uses hooks in production now so I'm pretty sure I can rely on them for my projects. Besides the enormity of React resources online there are a growing number of npm packages containing useful hooks, tools and other resources that can be found on the [awesome-react-hooks](https://github.com/rehooks/awesome-react-hooks) GitHub page.

## So...

There will never be a shortage of things to learn on the development front! One of the most difficult things it to figure out what NOT to learn as there are so many new things clamouring for attention. In my humble opinion both GraphQL and React Hooks are certainly worthy of attention. They certainly have mine.

Have fun and don't forget to stretch!

