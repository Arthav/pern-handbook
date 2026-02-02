# State Management

## 1. Types of State
1.  **Client State**: UI state (is modal open? is sidebar collapsed?). Best handled by `useState` or **Zustand**.
2.  **Server State**: Data from the DB (list of users). Best handled by **TanStack Query**.

## 2. TanStack Query (React Query)
The industry standard for fetching. It handles caching, retrying, and synchronization.

```tsx
import { useQuery } from '@tanstack/react-query';

const fetchUsers = async () => {
  const res = await fetch('/api/users');
  return res.json();
};

const UserList = () => {
  const { data, isLoading, error } = useQuery({
    queryKey: ['users'], 
    queryFn: fetchUsers,
    staleTime: 1000 * 60, // Data is fresh for 1 minute
  });

  if (isLoading) return <Spinner />;
  if (error) return <Text>Error!</Text>;

  return <div>{data.map(u => <User key={u.id} user={u} />)}</div>;
};
```

## 3. Zustand (Global Client State)
Redux is often overkill. Zustand is simple.

```tsx
import { create } from 'zustand';

const useStore = create((set) => ({
  isDarkMode: false,
  toggleTheme: () => set((state) => ({ isDarkMode: !state.isDarkMode })),
}));

// Usage
const App = () => {
  const { isDarkMode, toggleTheme } = useStore();
  return <button onClick={toggleTheme}>{isDarkMode ? '🌙' : '☀️'}</button>;
};
```

---
[← Previous Section](./02-hooks-deep-dive.md) | [Next Section →](../04-full-stack-integration/01-api-design.md)
