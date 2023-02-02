# Getting Started with Create React App

This project was bootstrapped with [Create React App](https://github.com/facebook/create-react-app).

## Redux class note

## Global state management
React state normally local state, to use them globally we need to create a context in react. 
Create a context first
`export const COUNTER_CONTEXT = createContext();`

Wrap the entire app by this context with value and provider
```<COUNTER_CONTEXT.Provider value={value}>
      <div className="App">
        <Parent></Parent>
      </div>
    </COUNTER_CONTEXT.Provider>```

Use the context where necessary
   ``` const { setCount, count } = useContext(COUNTER_CONTEXT);```

No need to props drilling to the child component. 


## Problem with handling multiple states useReducer()
useReducer is a hook, it take two parameter 
1. Reduce function 
2. initialState
Return state and dispatch function which have an action as object and it have action type must. Template is given below, 

```import React, { useContext, useReducer } from 'react';
import { COUNTER_CONTEXT } from '../App';


const Child = () => {
    // const { setCount, count } = useContext(COUNTER_CONTEXT);
    const initialState = 3;
    const reducer = (state, action) => {
        if (action.type === "INCREMENT") {
            return state + 1;
        } else if (action.type === "DECREMENT") {
            return state - 1;
        }
    }
```

  ```  const [state, dispatch] = useReducer(reducer, initialState)
    return (
        <div style={{ background: 'yellow' }}>
            <h1>{state}</h1>
            <div>
                <button
                    // onClick={() => { setCount(count + 1) }}
                    onClick={() => dispatch({ type: 'INCREMENT' })}
                >increase</button>
                <button
                    // onClick={() => { setCount(count - 1) }}
                    onClick={() => dispatch({ type: 'DECREMENT' })}
                >decrease</button>
            </div>
        </div>
    );
};


export default Child;```


