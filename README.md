===============================
LIBRARIES
===============================

- use-immer
  - useImmer
  - useImmerReducer

- react-router-dom
  - Declarative routing
  - Data routing
  - Data APIs (loader, action, fetcher)

- react-hook-form
  - useForm
  - useFieldArray

- yup
  - Schema validation

- @hookform/resolvers
- Axios

===============================
REACT HOOKS
===============================

Core Hooks:
- useState
- useEffect
- useReducer
- useRef
- useContext

Advanced / Performance:
- useMemo
- useCallback
- React.memo

Routing / Special:
- useLocation
- useNavigation
- useEffectEvent

Immer:
- useImmer
- useImmerReducer

Custom:
- Custom Hooks

===============================
ROUTING & UI UTILITIES
===============================

- scrollToHash component
  (for in-page routing / scrolling)

===============================
API & ARCHITECTURE
===============================

CRUD Operations:
- Create  → POST
- Read    → GET
- Update  → PUT / PATCH
- Delete  → DELETE

REST:
- Representational State Transfer

===============================
REACT ROUTER DATA APIS
===============================

Use loader and action instead of useEffect for API calls.

Rules:
- loader  → READ (GET)
- action  → WRITE (POST / PUT / DELETE)

Error handling:
- errorElement instead of try/catch
- useRouteError hook

Optimistic UI:
- Update UI immediately
- Background action continues
- Best for large data APIs

--------------------------------
ROUTE CONFIG EXAMPLE
--------------------------------
{
  path: "/users",
  element: <Users />,
  loader: usersLoader,
  errorElement: <UsersError />,
}

===============================
THREE WAYS TO CALL ACTION
===============================

Situation                            Best Choice
--------------------------------------------------
Login / Create / Save + redirect     <Form> (react-router-dom)
Delete button in list                fetcher.submit()
Edit inside modal                    <fetcher.Form>

===============================
PENDING / LOADING UI
===============================

const navigation = useNavigation();
const isLoading = navigation.state === "loading";

return (
  <>
    {isLoading && <p>Loading users...</p>}
    {/* rest UI */}
  </>
);

===============================
UI HELPERS
===============================

- React Spinner websites (for loaders)

- JavaScript operators:
  &&   ?:   ??   ||

===============================
IMPORTANT REACT RULES & NOTES
===============================

--------------------------------
1) Arrow Function Return Rule
--------------------------------
If you use {} in arrow functions, you MUST use return.
Or use () for implicit return.

const listItems = chemists.map(person =>
  <li>...</li>
);

OR

const listItems = chemists.map(person => (
  <li>...</li>
));

OR

const listItems = chemists.map(person => {
  return <li>...</li>;
});

--------------------------------
2) Keys in Lists
--------------------------------
Each list item must have a unique key.

<li key={person.id}>...</li>

Fragments example:

import { Fragment } from "react";

const listItems = people.map(person =>
  <Fragment key={person.id}>
    <h1>{person.name}</h1>
    <p>{person.bio}</p>
  </Fragment>
);

--------------------------------
3) Rules of Hooks
--------------------------------
- Hooks can only be called inside React components
- Hooks must be called at the top level
- Hooks cannot be conditional

--------------------------------
4) Immer vs React State
--------------------------------
- useImmer ≈ useState (objects & arrays only)
- useReducer ≈ useImmerReducer
- Immer allows mutating syntax (push, update)

--------------------------------
5) State Updater Function
--------------------------------
React queues updater functions.

<button onClick={() => {
  setNumber(n => n + 1);
  setNumber(n => n + 1);
  setNumber(n => n + 1);
}}>
  +3
</button>

Result increments one-by-one to +3.

Rules:
- Updaters must be pure
- No side effects inside updater

--------------------------------
6) Event Naming
--------------------------------
Don’t always use `e`
Use meaningful names when possible

--------------------------------
7) useEffect Dependencies Rule
--------------------------------
Do NOT use effect to update state derived from props/state.
It causes infinite re-renders.

--------------------------------
8) Static vs Dynamic in Effects
--------------------------------
- Move static objects/functions OUTSIDE component
- Move dynamic objects/functions INSIDE effect
- Helps avoid unnecessary dependencies

--------------------------------
9) useReducer Notes
--------------------------------
- Object passed to dispatch is called an action
- useReducer requires an initial value (null or initialState)
- useReducer ≈ useImmerReducer

--------------------------------
10) React Portal
--------------------------------
createPortal allows rendering a React element
outside the normal DOM hierarchy.

Used for:
- Modals
- Tooltips
- Dialog boxes
- Dropdowns

React Portal allows you to render a component
outside the normal DOM hierarchy of its parent component.

Portal ≠ Modal
Portal = Rendering outside normal DOM hierarchy

==> CONVERT MODAL TO PORTAL
Keep the same state logic.
Wrap modal JSX inside ReactDOM.createPortal
Target a separate DOM node.

--------------------------------
11) React Suspense
--------------------------------
Suspense lets you show fallback UI
while code or data is loading.

--------------------------------
12) Lazy Loading
--------------------------------
lazy() delays loading a component
until it is needed.

The function passed to lazy()
must return a Promise resolving
to a default exported component.

--------------------------------
13) React Router
--------------------------------
React Router provides routing for React apps.

It allows:
- Multiple pages in SPA
- URL params & query strings
- Browser navigation
- Nested routes & layouts
- Protected routes

--------------------------------
14) Layout Routes
--------------------------------
Layout Route (Parent Route):
- Provides shared UI (navbar, sidebar, footer)
- Does NOT represent a page
- Renders children using <Outlet />

Reference: App.jsx
