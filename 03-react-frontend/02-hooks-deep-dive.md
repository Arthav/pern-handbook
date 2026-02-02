# React Hooks: A Deep Dive

Beyond `useState` and `useEffect`.

## 1. `useMemo` & `useCallback`
These are performance optimizations. Don't use them prematurely.

### `useMemo`
Caches the **result** of a calculation.

```tsx
// Only re-calculate 'expensiveValue' if 'a' or 'b' change.
const expensiveValue = useMemo(() => computeExpensiveValue(a, b), [a, b]);
```

### `useCallback`
Caches the **function definition** itself. Crucial when passing functions as props to `React.memo` components.

```tsx
const handleClick = useCallback(() => {
  console.log('Clicked');
}, []); // Function reference stays the same between renders
```

## 2. Custom Hooks
The secret weapon of senior React devs. Extract logic from UI.

### Example: `useAuth`
Instead of checking tokens inside components, build a hook.

```tsx
// hooks/useAuth.ts
export const useAuth = () => {
  const [user, setUser] = useState(null);

  const login = async (creds) => {
    const data = await api.post('/login', creds);
    setUser(data.user);
    localStorage.setItem('token', data.token);
  };

  return { user, login };
};
```

---
[← Previous Section](./01-react-foundations.md) | [Next Section →](./03-state-management.md)
