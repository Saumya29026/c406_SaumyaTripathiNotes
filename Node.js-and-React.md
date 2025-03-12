# Node.js
### Definition
Node.js is an open-source, cross-platform JavaScript runtime environment that allows developers to execute JavaScript code outside of a web browser. It is built on Chrome's V8 JavaScript engine and uses an event-driven, non-blocking I/O model, making it lightweight and efficient.

## History
- 2009: Node.js was created by Ryan Dahl.
- 2010: npm (Node Package Manager) was introduced, making it easier to share and manage packages.
- 2015: The Node.js Foundation was formed to support the growth of the ecosystem.
- 2020: Node.js 14.x was released with improved performance and stability.

## Why Node.js?
- JavaScript Everywhere: Use the same language (JavaScript) for both frontend and backend development.
- High Performance: Non-blocking I/O and event-driven architecture make it ideal for real-time applications.
- Rich Ecosystem: npm provides access to thousands of reusable packages.
- Scalability: Designed to handle a large number of simultaneous connections.

# React
### Definition
React is an open-source JavaScript library for building user interfaces, particularly single-page applications (SPAs). It is maintained by Facebook and a community of developers. React allows developers to create reusable UI components and manage the state of their applications efficiently.

## History
- 2011: React was first deployed on Facebook's newsfeed.
- 2013: React was open-sourced at JSConf US.
- 2015: React Native was introduced, enabling mobile app development with React.
- 2019: React Hooks were introduced, simplifying state management and side effects.

### Why React?
- Component-Based Architecture: Build encapsulated components that manage their own state.
- Virtual DOM: Efficiently update and render only the necessary parts of the UI.
- Declarative Syntax: Write code that is easy to read and debug.
- Strong Community: Extensive resources, tutorials, and third-party libraries.

### How Node.js and React Work Together
- Node.js and React are often used together to build full-stack JavaScript applications:
- Backend (Node.js): Handles server-side logic, database interactions, and API endpoints.
- Frontend (React): Manages the user interface and client-side logic.
- Communication: The frontend (React) communicates with the backend (Node.js) via REST APIs or GraphQL.

## Coding Part

## Components
- **Counter.js**: A component to increment, decrement, and reset a counter.
- **Todo.js**: A component to add and display tasks.
- **ThemeSwitcher.js**: A button to toggle between light and dark themes.
- **PersonalInfoTable.js**: A form to input and display personal details.

## Pages
- **Home.js**: The home page with navigation to the About page.
- **About.js**: The About page with a simple description.

## How to Run the App
1. Install dependencies:
   ```bash
   npm install
   ```

## Components
### PersonalInfoTable
A form to input and display personal details (name, number, address, email).

```javascript
// src/components/PersonalInfoTable.js
import React, { useState } from 'react';

const PersonalInfoTable = () => {
  const [entries, setEntries] = useState([]);
  const [name, setName] = useState('');
  const [number, setNumber] = useState('');
  const [address, setAddress] = useState('');
  const [email, setEmail] = useState('');

  const handleSubmit = (e) => {
    e.preventDefault();
    if (name && number && address && email) {
      setEntries([...entries, { name, number, address, email }]);
      setName('');
      setNumber('');
      setAddress('');
      setEmail('');
    }
  };

  return (
    <div>
      <h2>Personal Information Form</h2>
      <form onSubmit={handleSubmit}>
        <input type="text" placeholder="Name" value={name} onChange={(e) => setName(e.target.value)} required />
        <input type="text" placeholder="Phone Number" value={number} onChange={(e) => setNumber(e.target.value)} required />
        <input type="text" placeholder="Address" value={address} onChange={(e) => setAddress(e.target.value)} required />
        <input type="email" placeholder="Email" value={email} onChange={(e) => setEmail(e.target.value)} required />
        <button type="submit">Add Entry</button>
      </form>

      <h3>Entries</h3>
      <table>
        <thead>
          <tr>
            <th>Name</th>
            <th>Phone Number</th>
            <th>Address</th>
            <th>Email</th>
          </tr>
        </thead>
        <tbody>
          {entries.map((entry, index) => (
            <tr key={index}>
              <td>{entry.name}</td>
              <td>{entry.number}</td>
              <td>{entry.address}</td>
              <td>{entry.email}</td>
            </tr>
          ))}
        </tbody>
      </table>
    </div>
  );
};

export default PersonalInfoTable;
```
## Counter
A component to increment, decrement, and reset a counter.

```javascript
// src/components/Counter.js
import React, { useState } from 'react';

const Counter = () => {
  const [count, setCount] = useState(0);

  const increment = () => setCount(count + 1);
  const decrement = () => setCount(count - 1);
  const reset = () => setCount(0);

  return (
    <div>
      <h2>Counter</h2>
      <p>Count: {count}</p>
      <button onClick={increment}>Increment</button>
      <button onClick={decrement}>Decrement</button>
      <button onClick={reset}>Reset</button>
    </div>
  );
};

export default Counter;
```
## Todo
A component to add and display tasks.

```javascript
// src/components/Todo.js
import React, { useState } from 'react';

const Todo = () => {
  const [tasks, setTasks] = useState([]);
  const [inputValue, setInputValue] = useState('');

  const addTask = () => {
    if (inputValue.trim()) {
      setTasks([...tasks, inputValue]);
      setInputValue('');
    }
  };

  return (
    <div>
      <h2>Todo List</h2>
      <input
        type="text"
        value={inputValue}
        onChange={(e) => setInputValue(e.target.value)}
        placeholder="Add a task"
      />
      <button onClick={addTask}>Add Task</button>
      <ul>
        {tasks.map((task, index) => (
          <li key={index}>{task}</li>
        ))}
      </ul>
    </div>
  );
};

export default Todo;
```
## ThemeSwitcher
A button to toggle between light and dark themes.

```javascript
// src/components/ThemeSwitcher.js
import React, { useState } from 'react';

const ThemeSwitcher = () => {
  const [theme, setTheme] = useState('light');

  const toggleTheme = () => {
    setTheme(theme === 'light' ? 'dark' : 'light');
  };

  return (
    <div>
      <button onClick={toggleTheme}>
        Switch to {theme === 'light' ? 'Dark' : 'Light'} Theme
      </button>
      <style>
        {`
          body {
            background-color: ${theme === 'light' ? '#ffffff' : '#333333'};
            color: ${theme === 'light' ? '#000000' : '#ffffff'};
          }
        `}
      </style>
    </div>
  );
};

export default ThemeSwitcher;
```
## Pages
### Home
The home page with navigation to the About page.

```javascript
// src/pages/Home.js
import { useNavigate } from 'react-router-dom';

function Home() {
  const navigate = useNavigate();

  return (
    <div>
      <h1>Home</h1>
      <button onClick={() => navigate('/about')}>Go to About</button>
    </div>
  );
}
export default Home;
```

### About
The About page with a simple description.

```javascript
// src/pages/About.js
function About() {
  return (
    <div>
      <h1>About</h1>
      <p>This is the About page.</p>
    </div>
  );
}

export default About;
  ```

## Routing
Routing is handled using react-router-dom. The App.js file sets up the routes for the application.

```javascript
// src/App.js
import React from 'react';
import { BrowserRouter as Router, Routes, Route, useNavigate } from 'react-router-dom';
import PersonalInfoTable from './components/PersonalInfoTable';
import Counter from './components/Counter';
import Todo from './components/Todo';
import ThemeSwitcher from './components/ThemeSwitcher';
import About from './pages/About';
import './App.css';

function App() {
  const navigate = useNavigate();

  return (
    <Router>
      <div className="App" style={{ backgroundColor: '#e6f7ff', minHeight: '100vh', padding: '20px' }}>
        <ThemeSwitcher />
        <div style={{ marginBottom: '20px' }}>
          <button onClick={() => navigate('/')}>Home</button>
          <button onClick={() => navigate('/about')}>About</button>
        </div>
        <Routes>
          <Route
            path="/"
            element={
              <>
                <h1 style={{ color: '#333', textAlign: 'center' }}>Personal Information Table</h1>
                <PersonalInfoTable />
                <h1>React Counter and Todo App</h1>
                <Counter />
                <Todo />
              </>
            }
          />
          <Route path="/about" element={<About />} />
        </Routes>
      </div>
    </Router>
  );
}

export default App;
```

### How to Run the App
1] Start the development server:

```bash
npm start
```
2] Open your browser and go to http://localhost:3000
