# Next.js: SSR, SSG, ISR – stručné vysvětlení

## Server Side Rendering (SSR)

**SSR** znamená, že stránka se renderuje na serveru při každém požadavku uživatele. Server vygeneruje HTML na základě aktuálních dat a odešle ho do prohlížeče.

- V Next.js použij funkci `getServerSideProps`.
- Vhodné, když potřebuješ vždy aktuální data (např. dashboard, profil uživatele).
- SEO friendly – vyhledávače dostanou hotové HTML.

```js
export async function getServerSideProps(context) {
  // Fetch data
  return { props: { data } }
}
```

---

## Static Site Generation (SSG)

**SSG** znamená, že stránka se vygeneruje do HTML během build procesu (tj. při nasazení aplikace), ne při každém požadavku. Výsledné HTML se uloží a servíruje uživatelům bez potřeby generování na serveru.

- V Next.js použij funkci `getStaticProps`.
- Výborné pro stránky, kde se data často nemění (např. blogové příspěvky, dokumentace).
- Rychlé načítání, skvělý výkon, nízké nároky na server.

```js
export async function getStaticProps(context) {
  // Fetch data
  return { props: { data } }
}
```

---

## Incremental Static Regeneration (ISR)

**ISR** je rozšíření SSG. Umožňuje znovu vygenerovat (aktualizovat) již staticky vygenerované stránky po určitém čase nebo na základě požadavku, aniž by bylo nutné znovu buildovat celou aplikaci.

- V Next.js použij také `getStaticProps`, ale přidej `revalidate`.
- Umožňuje kombinovat výhody statických stránek a aktualizovaných dat.
- Stránky se automaticky regenerují na pozadí, když uplyne interval `revalidate`.

```js
export async function getStaticProps(context) {
  // Fetch data
  return {
    props: { data },
    revalidate: 60, // stránka se obnoví max. každých 60 sekund
  }
}
```

---

## Shrnutí:

| Technika | Kdy se generuje HTML      | Výhoda                  | Vhodné použití                    |
|----------|--------------------------|-------------------------|-----------------------------------|
| SSR      | Při každém requestu      | Vždy aktuální data      | Dynamické stránky, personalizace  |
| SSG      | Při buildu               | Rychlost, levný provoz  | Blogy, dokumentace, statické stránky |
| ISR      | Při buildu + po čase     | Kombinace SSG a SSR     | Stránky, co se občas mění, ale mají být rychlé |

# Klíčové vlastnosti Next.js

1. **Server-side rendering (SSR)**
    - Možnost generovat stránky na serveru při každém požadavku.

2. **Static site generation (SSG)**
    - Generování statických stránek při buildu, vhodné pro rychlé a bezpečné weby.

3. **Incremental Static Regeneration (ISR)**
    - Obnova statických stránek po určitém čase bez nutnosti znovu buildovat celý web.

4. **API Routes**
    - Možnost vytvářet serverless API endpointy přímo ve stejném projektu.

5. **Routing založený na souborové struktuře**
    - Automatické generování rout na základě struktury složky `/pages` (nebo `/app` v nové architektuře).

6. **Podpora TypeScriptu**
    - Plná integrace s TypeScriptem bez složité konfigurace.

7. **Podpora CSS a CSS-in-JS**
    - Možnost používat globální i modulární CSS, stejně jako styled-components nebo emotion.

8. **Optimalizace obrázků (`next/image`)**
    - Automatická optimalizace a lazy loading obrázků.

9. **Built-in internationalization (i18n)**
    - Snadná správa vícejazyčných webů.

10. **Hot Reloading a Fast Refresh**
    - Okamžité zobrazení změn při vývoji bez ztráty stavu komponent.

11. **Podpora middlewarů**
    - Možnost psát middleware pro úpravu requestů a response.

12. **Deployment a hosting na Vercel**
    - Bezproblémové nasazení na platformu Vercel, ale Next.js lze nasadit i jinde (např. Netlify, AWS, vlastní server).

13. **Integrace s Reactem**
    - Next.js je postaven na Reactu a využívá jeho ekosystém.

14. **Podpora dynamických a parametrizovaných rout**
    - Generování stránek na základě dynamických parametrů v URL.

---
Pokud chceš některou z těchto vlastností rozvést, dej vědět!

# SPA vs. Fullstack Framework (React vs. Next.js)

## 1. Co je SPA (Single Page Application)?
- **SPA** je webová aplikace, která se načte jako jedna HTML stránka a následné navigace probíhají bez opětovného načtení stránky.
- Typickým příkladem je aplikace napsaná v čistém **Reactu** (např. vytvořená pomocí [Create React App](https://create-react-app.dev/)).

### Výhody SPA (React):
- **Rychlá uživatelská zkušenost:** Navigace mezi stránkami je okamžitá, protože se stránka nepřenačítá.
- **Jednodušší frontendová architektura:** Vše běží v prohlížeči, backend je často pouze API.
- **Dobrá pro komplexní interaktivní aplikace** (např. dashboardy).

### Nevýhody SPA:
- **SEO:** Vyhledávače nemusí dobře indexovat obsah, protože většina obsahu je generovaná až v prohlížeči.
- **Dlouhá doba prvního načtení:** Celá aplikace se musí stáhnout do prohlížeče hned na začátku.
- **Hůře řešitelná autentizace a ochrana citlivých dat.**

---

## 2. Co je Fullstack framework (např. Next.js)?
- **Fullstack framework** jako Next.js kombinuje frontend (React) a backend (serverové routy, SSR, SSG, API).
- Next.js umožňuje **server-side rendering (SSR)**, **static site generation (SSG)**, API endpoints atd.

### Výhody Next.js (Fullstack):
- **SEO:** Serverem generované (nebo staticky generované) stránky jsou snadno indexovatelné vyhledávači.
- **Rychlé načtení první stránky:** První obsah je vygenerován už na serveru.
- **Možnost backendových funkcí:** API routy, serverová logika, autentizace.
- **Flexibilita: SSR, SSG, ISR, CSR** – lze kombinovat různé strategie generování obsahu.
- **Lepší bezpečnost:** Citlivá logika zůstává na serveru.

### Nevýhody Next.js:
- **Složitější architektura:** Nutnost řešit jak serverovou, tak klientskou část.
- **Nasazování:** Vyžaduje hosting, který umí běžet Node.js server (nebo edge functions).
- **Občas vyšší komplexita vývoje** u malých projektů.

---

## 3. Ilustrační obrázky rozdělení

### SPA (React)

```mermaid
flowchart LR
    Browser --"Stáhne vše (JS, HTML, CSS)"--> ReactApp
    ReactApp --"API dotazy"--> Backend
```

- Frontend (React app) běží celý v prohlížeči, komunikuje pouze s API.

---

### Fullstack (Next.js)

```mermaid
flowchart LR
    Browser --"Požadavek na stránku"--> NextServer
    NextServer --"Vyrenderuje HTML (SSR/SSG/ISR)"--> Browser
    NextServer --"API dotazy"--> Backend
```

- Požadavek jde na server, který může stránku před-renderovat, případně poskytuje vlastní API.

---

## 4. Shrnutí hlavních rozdílů

| Vlastnost         | SPA (React)             | Fullstack (Next.js)          |
|-------------------|-------------------------|------------------------------|
| SEO               | Slabší                  | Výborné                      |
| První načtení     | Pomalejší               | Rychlejší                    |
| Navigace          | Okamžitá                | Okamžitá                     |
| Backend           | Potřebuješ zvlášť       | Součástí frameworku          |
| Nasazení          | Jednoduché (static host)| Složitější (server/edge)     |
| Komplexita        | Nižší                   | Vyšší                        |

---

Pokud chceš detailnější příklady nebo máš konkrétní dotaz, dej vědět!

# Klientská vs. serverová strana (client-side vs. server-side)

## 1. Klientská strana (Client-side)
- Kód běží v prohlížeči uživatele (JavaScript, HTML, CSS).
- Uživatelská interakce, dynamické změny na stránce, validace formulářů apod.
- Data se často stahují z API a zpracovávají až v prohlížeči.
- Příklad: SPA v Reactu, kde server posílá pouze základní HTML a JS.

### Výhody:
- Rychlé reakce na uživatelské akce (bez nutnosti komunikace se serverem).
- Nižší zatížení serveru.
- Bohaté, interaktivní UI.

### Nevýhody:
- Horší SEO (vyhledávač nemusí vidět obsah).
- Delší čas načtení první stránky (musí se stáhnout JS aplikace).
- Citlivý kód je vystaven uživateli.

---

## 2. Serverová strana (Server-side)
- Kód běží na serveru (např. Node.js, PHP, Python).
- Server vygeneruje kompletní HTML pro každou stránku a pošle ho klientovi.
- Příklad: SSR v Next.js nebo klasické PHP stránky.

### Výhody:
- Výborné SEO (vyhledávač vidí hotový obsah).
- Rychlé načtení první stránky.
- Možnost schovat citlivou logiku na serveru.

### Nevýhody:
- Vyšší zatížení serveru.
- Pomalejší reakce na některé uživatelské akce (nutnost komunikace se serverem).
- Méně interaktivní UI (pokud se vše řeší serverem).

---

## 3. Infografika

### Porovnání datového toku

#### Client-side rendering (CSR)
```mermaid
flowchart LR
    User["Uživatelův prohlížeč"] -- "Stáhne HTML/JS/CSS" --> Server
    User -- "API dotazy" --> API["Backend/API"]
    User -- "Renderuje UI" --> User
```

#### Server-side rendering (SSR)
```mermaid
flowchart LR
    User["Uživatelův prohlížeč"] -- "Požadavek na stránku" --> Server
    Server -- "Načte data z API/DB" --> API["Backend/API"]
    Server -- "Hotové HTML" --> User
```

---

## 4. Shrnutí hlavních rozdílů

| Vlastnost        | Klientská strana (CSR)  | Serverová strana (SSR)    |
|------------------|-------------------------|---------------------------|
| Kde běží kód     | V prohlížeči uživatele  | Na serveru                |
| První načtení    | Pomalejší               | Rychlejší                 |
| SEO              | Slabší                  | Výborné                   |
| Interaktivita    | Výborná                 | Omezená                   |
| Zatížení serveru | Nízké                   | Vyšší                     |

---

Pokud chceš konkrétní příklad v Reactu nebo Next.js, dej vědět!

# Rozdíly mezi prostředím Prohlížeč vs. Node.js
*v kontextu JavaScriptu, Reactu a Next.js*

---

## Prohlížeč (Browser)
- **Kde běží:** Uživatelův prohlížeč (Chrome, Firefox, Edge…)
- **Použití:** Frontend – vykreslování UI, interakce s uživatelem
- **API:** Má přístup k webovým API (např. `window`, `document`, `localStorage`, `fetch`)
- **DOM:** Může měnit DOM a vykreslovat komponenty Reactu
- **Bezpečnost:** Omezený přístup kvůli bezpečnosti (sandbox)
- **React:**
    - React komponenty se vykreslují do DOMu (`ReactDOM.render`)
    - V čistém Reactu (např. Create React App) vše běží pouze v prohlížeči – tzv. **Client-side rendering (CSR)**
- **Next.js:**
    - Next.js může také renderovat komponenty až v prohlížeči (**hydratuje** již připravený HTML)

---

## Node.js (Server)
- **Kde běží:** Server, backend, lokální CLI
- **Použití:** Zpracování požadavků, práce se soubory, API, serverová logika
- **API:** Má přístup k souborovému systému (`fs`), síti (`http`), procesům (`process`), ale **nemá** přístup k DOM, `window` ani `document`
- **DOM:** Neexistuje; nelze měnit stránku, pouze připravovat data/HTML
- **React:**
    - V Node.js lze React komponenty vykreslit do HTML na serveru (SSR) pomocí `ReactDOMServer.renderToString`
- **Next.js:**
    - Next.js používá Node.js ke **generování HTML na serveru** (SSR, SSG, ISR)
    - Serverová část Next.js může obsahovat API routy, přístup k databázi apod.

---

## Praktické rozdíly v React a Next.js

| Prostředí      | Má DOM / webová API | Přístup k serveru | Typický use-case         | Příklad kódu           |
|----------------|---------------------|-------------------|--------------------------|------------------------|
| Prohlížeč      | Ano                 | Ne                | UI, interakce            | `useEffect`, `fetch`   |
| Node.js        | Ne                  | Ano               | SSR, API, generování dat | `getServerSideProps`, `fs.readFile` |

---

## Infografika

### Next.js (Server i klient)

```
+---------------------------+
|         Uživatel          |
|  +---------------------+  |
|  |  Prohlížeč (React)  |  |   ←  HTML, JS, CSS z Next.js
|  +---------------------+  |
+---------------------------+
            ↑
            | HTTP(S)
            ↓
+---------------------------+
|       Server (Node.js)    | ← SSR, SSG, API, DB
|   - React (renderToString)|
|   - Next.js API routes    |
|   - Práce se soubory      |
+---------------------------+
```

---

## Shrnutí

- **Prohlížeč:** Spouští UI, React běží proti DOMu (CSR/Hydratace), omezený přístup (žádný filesystem, žádný přímý přístup k serveru).
- **Node.js:** Spouští serverovou logiku, generuje HTML (SSR/SSG v Next.js), má přístup k souborům, DB, může zpracovávat API požadavky, ale **nemá DOM**.

---

*Chceš-li příklad rozdílu v kódu (např. fetchování dat na serveru vs. v prohlížeči), dej vědět!*
