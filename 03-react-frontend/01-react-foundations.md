# React Foundations for PERN

Creating a frontend that talks to your Express backend.

## 1. Project Setup (Vite)
Don't use `create-react-app` (it's deprecated/slow). Use Vite.

```bash
npm create vite@latest my-app -- --template react-ts
```

## 2. The Mental Model
React is **Declarative**. You tell it *what* the UI should look like for a given state, and React handles the DOM updates.

> UI = f(State)

## 3. Communication with Express
React runs in the browser (port 5173). Express runs on the server (port 3000). They are on different domains.

### Fetching Data (`useEffect`)
The classic beginner way.

```tsx
const UserList = () => {
  const [users, setUsers] = useState([]);

  useEffect(() => {
    fetch('http://localhost:3000/api/users')
      .then(res => res.json())
      .then(data => setUsers(data));
  }, []); // [] = Run once on mount

  return (
    <ul>
      {users.map(u => <li key={u.id}>{u.username}</li>)}
    </ul>
  );
};
```

**Why this is bad for production:**
1.  **Race Conditions**: If the component unmounts before fetch finishes, it errors.
2.  **Caching**: It refetches every time you visit the page.
3.  **Loading States**: You have to manually manage `isLoading` and `isError`.
4.  **Waterfalls**: Fetching child data only after parent finishes.

**The Solution?** TanStack Query (in the State Management section).
