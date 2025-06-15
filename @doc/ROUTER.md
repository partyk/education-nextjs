# Rozdíl mezi App Router a Pages Router v Next.js

## Pages Router (starší způsob)
- **Složka:** `/pages`
- **Routing:** Každý soubor v adresáři `/pages` automaticky tvoří routu (např. `/pages/about.js` = `/about`).
- **Data fetching:** Pomocí funkcí `getStaticProps`, `getServerSideProps`, `getInitialProps`.
- **Rendering:** Podporuje SSR, SSG, ISR i CSR.
- **API routes:** V `/pages/api` lze přímo vytvářet API endpointy.
- **File-based routing:** Routing je odvozený čistě ze struktury souborů.
- **React:** Používá React funkční komponenty, není nativní podpora pro React Server Components.
- **Layouty:** Layouty nejsou vestavěné, musíš je řešit ručně (např. v `_app.js`).
- **Použití:** Stabilní, široce používaný způsob do Next.js 13+.

---

## App Router (novější způsob, od Next.js 13)
- **Složka:** `/app`
- **Routing:** Každý adresář v `/app` může obsahovat soubor `page.js` (nebo `page.tsx`), který tvoří routu (např. `/app/about/page.js` = `/about`).
- **Data fetching:** Pomocí `fetch`, async komponent, server actions atd. (nepoužívá `getStaticProps` atd.).
- **Rendering:** Nativní podpora pro React Server Components (RSC) – část kódu běží na serveru, část na klientovi.
- **Layouty:** Vestavěná podpora layoutů (`layout.js` v každé složce).
- **Loading a error states:** Vestavěné řešení přes soubory `loading.js`, `error.js`.
- **API routes:** Zůstávají zatím v `/pages/api`.
- **Flexibilita:** Lépe řeší složitější aplikace, nested layouts, paralelní routes, streaming.
- **Budoucnost Next.js:** App Router je doporučovaný způsob pro nové projekty.

---

## Praktické shrnutí rozdílů

| Vlastnost           | Pages Router (`/pages`)   | App Router (`/app`)         |
|---------------------|--------------------------|-----------------------------|
| Umístění kódu       | `/pages`                 | `/app`                      |
| Routing             | Soubor = route           | Složka + `page.js` = route  |
| Layouty             | Vlastní řešení           | Vestavěná podpora `layout.js`|
| Data fetching       | `getStaticProps`, ...    | `fetch`, async/await, RSC   |
| React Server Components | Ne                    | Ano                         |
| Nested routing      | Omezené                  | Výborné (složky v složkách) |
| API routes          | `/pages/api`             | Zatím stále `/pages/api`    |
| Použití             | Starší projekty, stabilní| Moderní, nové projekty      |

---

## Infografika

```
Struktura Pages Router:
/pages
  |-- index.js      => /
  |-- about.js      => /about
  |-- blog/[id].js  => /blog/123

Struktura App Router:
/app
  |-- page.js           => /
  |-- about/
        |-- page.js     => /about
        |-- layout.js   => layout pro /about
  |-- blog/
        |-- [id]/
              |-- page.js   => /blog/123
```

---

## Doporučení
- **Nové projekty:** používej App Router (`/app`) – je výchozí volbou, podporuje nejnovější funkce Next.js a Reactu.
- **Starší projekty:** Pages Router je stále podporovaný a stabilní, nemusíš ihned migrovat.

---

*Chceš-li příklad kódu nebo konkrétní porovnání, napiš!*
