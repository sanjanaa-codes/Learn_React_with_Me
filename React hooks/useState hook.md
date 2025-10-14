
-> The useState hook’s return value in React is the array data structure.  
-> The useState hook allows you to work with state in components.   
-> The useState hook invocation returns a two-member array - When calling the useState() hook, 
the returned array holds the state variable's value asthe first item of that array and the 
function that will be used to update the stateas the second item of that returned array.  
-> When using the useState hook, there is only one correct way to update state when using useState and that’s through 
the state-updating function. 

  An example of holding state in an object and updating it based on user-generated events
When you need to hold state in an object and update it, initially, you might try something like this:

__________________________________________________________________________________________________

import { useState } from "react"; 
 
export default function App() { 
  const [greeting, setGreeting] = useState({ greet: "Hello, World" }); 
  console.log(greeting, setGreeting); 
 
  function updateGreeting() { 
    setGreeting({ greet: "Hello, World-Wide Web" }); 
  } 
 
  return ( 
    <div> 
      <h1>{greeting.greet}</h1> 
      <button onClick={updateGreeting}>Update greeting</button> 
    </div> 
  ); 
}
__________________________________________________________________________________________________
-> While this works, it's not the recommended way of working with state objects in React, this is because the state object usually 
has more than a single property, and it is costly to update the entire object just for the sake of updating only a small part of it.

-> The correct way to update the state object in React when using useState:

-> The suggested approach for updating the state object in React when using useState is to copy the state object and then update the copy.
This usually involves using the spread operator (...).
  
Keeping this in mind, here's the updated code:
__________________________________________________________________________________________________

import { useState } from "react"; 
 
export default function App() { 
  const [greeting, setGreeting] = useState({ greet: "Hello, World" }); 
  console.log(greeting, setGreeting); 
 
  function updateGreeting() { 
    const newGreeting = {...greeting}; 
    newGreeting.greet = "Hello, World-Wide Web"; 
    setGreeting(newGreeting); 
  } 
 
  return ( 
    <div> 
      <h1>{greeting.greet}</h1> 
      <button onClick={updateGreeting}>Update greeting</button> 
    </div> 
  ); 
} 
__________________________________________________________________________________________________
Incorrect ways of trying to update the state object
To prove that a copy of the old state object is needed to update state, 
let’s explore what happens when you try to update the old state object directly:

import { useState } from "react"; 
 
export default function App() { 
  const [greeting, setGreeting] = useState({ greet: "Hello, World" }); 
  console.log(greeting, setGreeting); 
 
  function updateGreeting() { 
    greeting = {greet: "Hello, World-Wide Web}; 
    setGreeting(greeting); 
  } 
 
  return ( 
    <div> 
      <h1>{greeting.greet}</h1> 
      <button onClick={updateGreeting}>Update greeting</button> 
    </div> 
  ); 
} 
__________________________________________________________________________________________________

The above code does not work because it has a TypeError hiding inside of it.
Specifically, the TypeError is: "Assignment to constant variable".
In other words, you cannot reassign a variable declared using const, such as in the case of the 
useState hook's array destructuring:

const [greeting, setGreeting] = useState({ greet: "Hello, World" }); 

Another approach you might attempt to use to work around the suggested way of updating state when working 
with a state object might be the following: 
__________________________________________________________________________________________________

import { useState } from "react"; 
 
export default function App() { 
  const [greeting, setGreeting] = useState({ greet: "Hello, World" }); 
  console.log(greeting, setGreeting); 
 
  function updateGreeting() { 
    greeting.greet = "Hello, World-Wide Web; 
    setGreeting(greeting); 
  } 
 
  return ( 
    <div> 
      <h1>{greeting.greet}</h1> 
      <button onClick={updateGreeting}>Update greeting</button> 
    </div> 
  ); 
} 
__________________________________________________________________________________________________
-> The above code is problematic because it doesn't throw any errors; however, it also doesn't update the heading, 
so it is not working correctly. This means that, regardless of how many times you click the "Update greeting" button, it will still be "Hello, World".
-> To reiterate, the proper way of working with state when it's saved as an object is to:
-> Copy the old state object using the spread (...) operator and save it into a new variable and 
-> Pass the new variable to the state-updating function 

-> Updating the state object using arrow functions
-> Now, let’s use a more complex object to update state.
-> The state object now has two properties: greet and location.
-> The intention of this update is to demonstrate what to do when only a specific property of the state object is changing, 
while keeping the remaining properties unchanged:
__________________________________________________________________________________________________

import { useState } from "react"; 
 
export default function App() { 
  const [greeting, setGreeting] = useState( 
    { 
        greet: "Hello", 
        place: "World" 
    } 
  ); 
  console.log(greeting, setGreeting); 
 
  function updateGreeting() { 
    setGreeting(prevState => { 
        return {...prevState, place: "World-Wide Web"} 
    }); 
  } 
 
  return ( 
    <div> 
      <h1>{greeting.greet}, {greeting.place}</h1> 
      <button onClick={updateGreeting}>Update greeting</button> 
    </div> 
  ); 
} 
__________________________________________________________________________________________________
The reason this works is because it uses the previous state, which is named prevState, and this is the previous 
value of the greeting variable. In other words, it makes a copy of the prevState object, and updates only the 
place property on the copied object. It then returns a brand-new object: 

return {...prevState, place: "World-Wide Web"} 

Everything is wrapped in curly braces so that this new object is built correctly, and it is returned from the call to setGreeting.

___________________________________________________________________________________________________
**React Data Flow — Little Lemon Goals App**

```
               🟨 Parent Component
               ┌────────────────────────────────┐
               │            App.jsx             │
               │--------------------------------│
               │ State:                         │
               │  const [allGoals, setAllGoals] │
               │   = useState([]);              │
               │                                │
               │ Function:                      │
               │  addGoal(goalEntry) {          │
               │    setAllGoals([...prevGoals,  │
               │                goalEntry]);    │
               │  }                             │
               │                                │
               │ Renders:                       │
               │  <GoalForm onAdd={addGoal}/>   │
               │  <ListOfGoals allGoals={...}/> │
               └────────────────────────────────┘
                         ▲             │
                         │ props.onAdd │ props.allGoals
                         │             ▼
      ┌───────────────────────────────┐       ┌───────────────────────────────┐
      │        GoalForm.jsx           │       │      ListOfGoals.jsx          │
      │-------------------------------│       │-------------------------------│
      │ State:                        │       │ Props:                        │
      │  formData = { goal: "", by:""}│       │  allGoals (array of objects)  │
      │                               │       │                               │
      │ User types → changeHandler()  │       │ Loops:                        │
      │  setFormData({...formData,    │       │  allGoals.map(goalObj =>      │
      │   [e.target.name]: e.target.value})   │   <li>{goalObj.goal} - {goalObj.by}</li>)│
      │                               │       └───────────────────────────────┘
      │ User clicks “Add Goal” → submitHandler()
      │  → props.onAdd(formData)  🔁 sends data up
      │  → setFormData({goal:"",by:""}) clears inputs
      └───────────────────────────────┘
```
🔄 **Step-by-Step Data Flow**

1. **User types** into input fields
   ➜ `changeHandler` updates `formData` using `setFormData()`.

2. **User clicks Submit**
   ➜ `submitHandler` calls `props.onAdd(formData)` (passed down from `App`).

3. **Data flows upward** to `App`
   ➜ `App` receives `goalEntry` and calls `setAllGoals()` to update the array.

4. **React re-renders**
   ➜ The updated `allGoals` array is passed down as a prop to `ListOfGoals`.

5. **ListOfGoals displays** the new goal in the list dynamically.

---
⚙️ Quick Example in Action

| Action                 | What Happens                |
| ---------------------- | --------------------------- |
| Type in inputs         | `formData` updates live     |
| Click “Add Goal”       | `addGoal()` runs in App     |
| App updates `allGoals` | UI re-renders with new goal |
| Form resets            | Inputs become empty again   |

---
_______________________________________________________________________________________________

Question 1
Is this a valid useState hook invocation and destructuring?

const [car, setCar] = useState({ color: 'blue', mileage: 0})

-> Yes
-> No
-> It would be valid, if it was spread over multiple lines.


Correct. This code shows a valid call to the useState() hook. It's also correctly destructured to car and setCar.
Ans-> Yes
-----------------------------------------------------------------------------------------------------------------
Question 2
True or False: You can clone a JS object using the . operator (the dot operator).


-> True
-> False

Correct. The dot operator is not used to clone an object in JS.
Ans-> False
------------------------------------------------------------------------------------------------------------------
Question 3
Consider the following code:

const [person, setPerson] = useState({ name: 'John', age: 21})

Imagine you're using a setPerson() state-updating function to update the value of the state variable named person. 
You only want to update the value of age, from 21 to 22. Choose the correct code snippet to do that.

-> setPerson(prev => ({ ...prev, age: 22 }));
-> setPerson(() => ({ age: 22 }));
-> setPerson(person.age = 22);


Correct
Yes, this snippet is correct, because it clones the previous state object, and updates only the cloned object's age value.
Ans-> setPerson(prev => ({ ...prev, age: 22 }));


  



