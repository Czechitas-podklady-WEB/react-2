## React router

V Reactu vytváříme primárně tzv. SPA (Single-page Application), kde se veškerá interakce s uživatelem děje v rámci jedné stránky a React jen aktualizuje její obsah.

Chceme-li naši aplikaci rozšířit na více stránek, musíme zařídit, aby při přechodu na novou stránku React aktualizoval obsah v prohlížeči. O to se postará například knihovna (React Router)[https://reactrouter.com/en/main].

Knihovnu musíme do naší aplikace doinstalovat pomocí NPM.

```sh
npm install react-router-dom
```

Nyní máme v aplikaci k dispozici množství komponent, se kterými můžeme pracovat. Nejprve je musíme v aplikaci naimportovat, jako každou jinou komponentu.

```jsx
import React from 'react'
import ReactDOM from 'react-dom/client'
import {
  createBrowserRouter,
  RouterProvider,
  Link,
  Outlet,
} from "react-router-dom";

// konfigurace routeru
const router = createBrowserRouter([
  {
    path: "/",
    element: <App />,
    children: [
      {
        path: 'about',
        element: <About />,
      },
      {
        path: 'Contact',
        element: <Contact />,
      },
    ]
  },
]);


function About() {
  return (
    <>
      <h2>About</h2>
      <p>Lorem ipsum...</p>
    </>
  );
}

function Contact() {
  return (
    <>
      <h2>Contact</h2>
      <p>Lorem ipsum...</p>
    </>
  );
}

const App = () => (
  <div>
    <h1>Super Store</h1>
    <nav>
      <Link to="/about">About</Link> |{' '}
      <Link to="/contact">Contact</Link>
    </nav>
    <main>
      <Outlet />
    </main>
  </div>
);

ReactDOM.createRoot(document.getElementById('root')).render(
  <React.StrictMode>
    <RouterProvider router={router} />
  </React.StrictMode>,
);
```

