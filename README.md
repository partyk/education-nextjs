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
