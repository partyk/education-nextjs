# Postup instalace Next.js

## 1. Předpoklady
- Měj nainstalovaný [Node.js](https://nodejs.org/) (doporučená verze 18+)
- Měj nainstalovaný [npm](https://www.npmjs.com/) nebo [yarn](https://yarnpkg.com/)

---

## 2. Vytvoření nového Next.js projektu

### Pomocí `npx` (doporučeno)
```bash
npx create-next-app@latest
```
- Interaktivně zadáš název projektu a další volby (TypeScript, ESLint, Tailwind, atd.)
- Nebo rovnou:
```bash
npx create-next-app@latest my-next-app
```

### Pomocí `yarn`
```bash
yarn create next-app my-next-app
```

---

## 3. Přechod do složky projektu
```bash
cd my-next-app
```

---

## 4. Spuštění vývojového serveru
```bash
npm run dev
```
nebo
```bash
yarn dev
```
- Aplikace běží na [http://localhost:3000](http://localhost:3000)

---

## 5. Další kroky
- Otevři projekt v preferovaném editoru (např. VS Code)
- Začni upravovat soubory v adresáři `/app` nebo `/pages` podle zvoleného typu routování

---

## 6. Rychlý přehled příkazů

| Příkaz                      | Popis                        |
|-----------------------------|------------------------------|
| `npm run dev`               | Spustí vývojový server       |
| `npm run build`             | Vytvoří produkční build      |
| `npm start`                 | Spustí produkční server      |

---

Více v oficiální dokumentaci: [https://nextjs.org/docs/getting-started/installation](https://nextjs.org/docs/getting-started/installation)
