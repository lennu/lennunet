---
title: Redux Action Creator vs. Action
date: 2017-02-27
redirect_from: /redux-action-creator-vs-action/
---
One of the core things in Redux is the **Actions**.

These are the things that you send to reducers which eventually change the state of the application.

Action -> Reducer -> State

Action
------

Usually actions are formed like this: (**This is a JavaScript object**)

```
{
 type: SET_NAME,
 name: 'John',
}
```

We have type and we have name.

**Type** is how Redux’s reducers know how they should modify the state and the second property **name** has the value we want to insert into our state.

Action Creator
--------------

So now we know what is an action (it’s a JavaScript Object), next we’d like to know how it’s different from **action creator**.

This is action creator:

```
function setName(name) {
  return {
    type: SET_NAME,
    name: name,
  }
}
```

See the middle part that returns an object, it’s the same JavaScript object we defined above. The difference between action and action creator is quite simple.

Action is the actual object that is sent for the Reducer.

Action creator is a function that is used to create this object.