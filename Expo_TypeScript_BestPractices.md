# 🧑‍💻 React Native + Expo SDK (TypeScript) Best Practices Guide

A complete guideline for writing clean, scalable, and maintainable React Native apps using **Expo SDK**, **TypeScript**, and **Expo Router**.

---

## 🗂️ Project Structure

```
MyApp/
├── app/                # Screens (routes with Expo Router)
│   ├── index.tsx
│   ├── about.tsx
│   └── [...404].tsx
├── components/         # Reusable UI components
│   └── Button.tsx
├── constants/          # App-wide constants (colors, fonts, etc.)
├── hooks/              # Custom hooks
├── lib/                # API clients, services, helpers
│   └── api.ts
├── types/              # Global types and interfaces
│   └── index.ts
├── assets/             # Fonts, images, etc.
├── app.config.ts       # Expo app configuration
└── tsconfig.json
```

---

## 🎨 Styling Guidelines

- Use **StyleSheet.create** or **Tailwind with NativeWind**
- Use constants from `constants/colors.ts`
- Always **prefer reusable styles** and avoid inline styles

### Example:

```tsx
import { StyleSheet, View, Text } from 'react-native';

const Welcome = () => (
  <View style={styles.container}>
    <Text style={styles.title}>Welcome!</Text>
  </View>
);

const styles = StyleSheet.create({
  container: {
    flex: 1,
    justifyContent: 'center',
    alignItems: 'center',
  },
  title: {
    fontSize: 24,
    fontWeight: 'bold',
  },
});
```

---

## 🔧 API Service Layer

- Keep all API logic in `/lib/api.ts`
- Always use async/await with try/catch

### Example:

```ts
// lib/api.ts
export const fetchUser = async () => {
  try {
    const res = await fetch('https://example.com/api/user');
    if (!res.ok) throw new Error('Failed to fetch user');
    return await res.json();
  } catch (error) {
    console.error('API Error:', error);
    throw error;
  }
};
```

---

## 🚨 Error Handling

- Use try/catch in async functions
- Show user-friendly messages using `Toast`, `Alert`, or `Snackbar`
- Avoid exposing technical errors

### Example:

```ts
import { Alert } from 'react-native';

const loadUser = async () => {
  try {
    const user = await fetchUser();
    setUser(user);
  } catch (error) {
    Alert.alert('Something went wrong. Please try again.');
  }
};
```

---

## 🧭 Navigation (Expo Router)

- Follow file-based routing with `/app`
- Use `Link` and `useRouter` for navigation

### Example:

```tsx
// app/index.tsx
import { Link } from 'expo-router';

export default function Home() {
  return <Link href="/about">Go to About</Link>;
}
```

```tsx
// app/about.tsx
import { useRouter } from 'expo-router';

export default function About() {
  const router = useRouter();
  return <Button title="Back" onPress={() => router.back()} />;
}
```

---

## 🧪 Best Practices

- Use TypeScript everywhere
- Prefer `const` over `let`
- Break UI into small components
- Avoid long files (>200 lines)
- Use `FlatList` for large scrollable data
- Organize constants/types/hooks logically
- Write unit tests for logic functions

---

## ✅ Sample Environment Setup

```bash
npx create-expo-app MyApp -t with-router --template
cd MyApp
npm install --save-dev typescript
npx expo install expo-router react-native-safe-area-context react-native-screens react-native-gesture-handler
```

---

## 📁 Constants Example

```ts
// constants/colors.ts
export const COLORS = {
  primary: '#1e90ff',
  secondary: '#ffcc00',
  text: '#333333',
};
```

---

## ✨ Useful Libraries

- `expo-router`
- `expo-font`
- `expo-secure-store`
- `zustand` (state management)
- `react-query` (server state)
- `yup` + `formik` or `react-hook-form` (form validation)
- `react-native-svg` (icons)

---

## 🤖 GitHub Copilot Prompts

> “Create a reusable Button component using TypeScript and StyleSheet.”  
> “Add error handling to an async API call using try/catch.”  
> “Generate a new Expo Router screen with a text input and button.”  
> “Create a form with validation using `formik` and `yup`.”

---

## 🔚 Final Notes

✅ Use TypeScript everywhere  
✅ Stick to consistent structure  
✅ Handle every async task carefully  
✅ Prefer components, constants, and services for reusability  
✅ Keep UI logic and business logic separate

---

_This markdown serves as a developer guide for scalable, professional apps using Expo Router + TypeScript._