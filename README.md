# `redux-immutable`

[![Travis build status](http://img.shields.io/travis/gajus/redux-immutable/master.svg?style=flat-square)](https://travis-ci.org/gajus/redux-immutable)
[![NPM version](http://img.shields.io/npm/v/redux-immutable.svg?style=flat-square)](https://www.npmjs.org/package/redux-immutable)
[![Canonical Code Style](https://img.shields.io/badge/code%20style-canonical-blue.svg?style=flat-square)](https://github.com/gajus/canonical)

`redux-immutable` is used to create an equivalent function of Redux [`combineReducers`](http://rackt.org/redux/docs/api/combineReducers.html) that works with [Immutable.js](https://facebook.github.io/immutable-js/) state.

When Redux [`createStore`](https://github.com/rackt/redux/blob/master/docs/api/createStore.md) `reducer` is created using `redux-immutable` then `initialState` must be an instance of [`Immutable.Iterable`](https://facebook.github.io/immutable-js/docs/#/Iterable).

## Problem

When [`createStore`](https://github.com/rackt/redux/blob/master/docs/api/createStore.md) is invoked with `initialState` that is an instance of `Immutable.Iterable` further invocation of reducer will [produce an error](https://github.com/rackt/redux/blob/v3.0.6/src/combineReducers.js#L31-L38):

> The initialState argument passed to createStore has unexpected type of "Object".
> Expected argument to be an object with the following keys: "data"

This is because Redux `combineReducers` [treats `state` object as a plain JavaScript object](https://github.com/rackt/redux/blob/v3.0.6/src/combineReducers.js#L120-L129).

`combineReducers` created using `redux-immutable` uses Immutable.js API to iterate the state.

## Usage

Create a store with `initialState` set to an instance of [`Immutable.Iterable`](https://facebook.github.io/immutable-js/docs/#/Iterable):

```js
import {
    combineReducers
} from 'redux-immutable';

import {
    createStore
} from 'redux';

let initialState,
    rootReducer,
    store;

initialState = Immutable.Map();

rootReducer = combineReducers({});

store = createStore(rootReducer, initialState);
```
