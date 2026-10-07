# 🧱 Dev Stack — Tech Stack Builder

Picking a tech stack for a new project always takes me longer than it should. I keep jumping between docs, comparing frameworks, and forgetting what I already decided on. So I built **Dev Stack**, a small web app where you can browse popular technologies, check their details at a glance, and put together your own stack in one place.

🔗 **Live Site:** [assignment-05-ruddy-seven.vercel.app](https://assignment-05-ruddy-seven.vercel.app/)

![Dev Stack screenshot](./screenshot.png)

---

## 🛠️ Technologies Used

- **React 19** for building the UI with components
- **TypeScript** to keep the data and props type safe
- **Tailwind CSS 4** and **daisyUI 5** for styling and layout
- **React-Toastify** for the little alert messages
- **JSON** file for storing all the technology data
- **Vite** as the build tool and dev server

---

## ✨ Features

1. **Browse technologies**
   All technologies are loaded from a JSON file and shown as cards. Each card has the icon, a short description, category, difficulty level and rating, so it's easy to compare them side by side.

2. **Build your own stack**
   Click "Add to Stack" on any card and it shows up in the "Your Stack" panel right next to the grid. The button changes to "✓ Added to Stack" so you know what's already picked, and if you try to add the same one again you'll get a warning.

3. **Remove anytime**
   Changed your mind? Remove a single item with the ✕ button, or clear everything at once with "Remove All". The panel goes back to its empty state when nothing is selected.

---

## 📦 Dependencies

| Package | Version | Purpose |
|---|---|---|
| `react` | ^19.2.8 | UI library |
| `react-dom` | ^19.2.8 | Renders React to the DOM |
| `react-toastify` | ^11.1.0 | Toast notifications |
| `tailwindcss` | ^4.3.3 | Utility-first CSS |
| `@tailwindcss/vite` | ^4.3.3 | Tailwind plugin for Vite |

**Dev dependencies:** `typescript`, `vite`, `@vitejs/plugin-react`, `daisyui`, `oxlint`, `@types/react`, `@types/react-dom`, `@types/node`

---

## 🚀 Run It Locally

**Prerequisites:** [Node.js](https://nodejs.org/) (v18 or later) and npm

```bash
# 1. Clone the repository
git clone https://github.com/devsuvo/Assignment-05.git

# 2. Go into the project folder
cd Assignment-05

# 3. Install dependencies
npm install

# 4. Start the development server
npm run dev
```

Then open `http://localhost:5173` in your browser.

To create a production build, run `npm run build`, then `npm run preview` to test it.

---

## 💡 What I Learned

This was my first time mixing TypeScript with React in a real project. Passing props between components and keeping the stack state in one place (App) took me a bit to figure out, but it made the add/remove logic much cleaner in the end.

<details>
<summary><b>📝 React Questions (click to expand)</b></summary>

<br/>

**1. What is JSX, and why is it used in React?**

JSX lets me write HTML-like code directly inside JavaScript. It's not real HTML, it gets converted to `React.createElement()` calls behind the scenes. I like it because I can see what the UI will look like right in the component, and I can drop JavaScript values into it with `{}`, like `{tech.name}` in my cards.

**2. What is the difference between props and state?**

Props are data a component receives from its parent, and the component can't change them. State is data a component owns and can change itself. In my project, `TechCard` gets `tech` and `isAdded` as props, while the `stack` array lives as state in `App` because it changes whenever the user adds or removes something.

**3. What does the `useState` hook do, and where did you use it in this project?**

`useState` gives a component a value that it can remember and update. When the value changes, React re-renders the component. I used it in `App.tsx` for `technologies`, `stack` and `loading`, and in `Navbar.tsx` for the active link and to open/close the mobile menu.

**4. What does the `useEffect` hook do, and why did you need it to load the JSON data?**

`useEffect` runs code after the component renders, which is the right place for side effects like fetching data. I used it to `fetch("/technologies.json")` once when the page loads (with an empty `[]` dependency array). If I fetched directly inside the component body, it would run on every render and cause an endless loop, since setting state triggers another render.

**5. Why does every item in a `.map()` list need a unique `key` prop?**

The key helps React tell list items apart, so when the list changes it knows exactly which item was added, removed or moved and only updates that one. I used each technology's `id` as the key (`key={tech.id}`). Using the array index can cause bugs when items get removed, like in my stack list.

**6. What is conditional rendering? Show one place you used it.**

It means showing different UI depending on a condition. In `StackSidebar.tsx`, if the stack is empty it shows "Your stack is empty.", otherwise it shows the list and the Remove All button:

```tsx
{count === 0 ? (
  <div>Your stack is empty.</div>
) : (
  <ul>{/* stack items */}</ul>
)}
```

I also used it on the card button, which reads "✓ Added to Stack" when `isAdded` is true.

**7. How do you pass data from parent to child, and how does a child send something back?**

Parent to child: through props. `App` passes `technologies` and `stack` down to `TechCatalog`, which passes each `tech` to `TechCard`.

Child to parent: the parent passes a function as a prop, and the child calls it. `App` gives `handleAddToStack` to `TechCard` as `onAdd`, and when the button is clicked the card calls `onAdd(tech)`, which sends that technology back up to `App` to update the stack.

---

Made by [devsuvo](https://github.com/devsuvo)

</details>

---

## 🔗 Links

- **Live Site:** [assignment-05-ruddy-seven.vercel.app](https://assignment-05-ruddy-seven.vercel.app/)
- **Repository:** [github.com/devsuvo/Assignment-05](https://github.com/devsuvo/Assignment-05)
- **Developer:** [Suvo Dev](https://github.com/devsuvo) · [Portfolio](https://suvo.dev) · [LinkedIn](https://www.linkedin.com/in/devsuvo/)
