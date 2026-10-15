# hinnovation.be — statische kopie

Deze map is een volledige, statische versie van www.hinnovation.be (NL + EN, 18 pagina's,
68 bestanden, ±16 MB). Ze is gemaakt op 15 oktober 2026 door de live site te kopiëren en is
visueel identiek: screenshots van alle hoofdpagina's op desktop (1440 px) en mobiel (390 px)
verschillen 0,000–0,003 % van de live site.

Er is geen CMS, database of PHP meer nodig. Elke host die statische bestanden serveert volstaat.

## Wat is er veranderd t.o.v. de live site

| Onderdeel | Live site (Craft CMS) | Deze kopie |
|---|---|---|
| Vormgeving, tekst, beelden, fonts | — | identiek |
| Contactformulier | Craft Express Forms (CSRF-token, server) | [Web3Forms](https://web3forms.com) — gratis, mails komen op het adres dat je bij registratie opgeeft |
| `cdn.polyfill.io` script | aanwezig | **verwijderd** (domein sinds 2024 in handen van een kwaadwillende partij; browsers blokkeren het) |
| Google Analytics | UA-179280493-1 (Universal Analytics, meet sinds juli 2023 niets meer) | verwijderd; GA4-id kan via `build_static.py` worden toegevoegd |
| Jaartal in footer | door Craft gegenereerd | klein JS-regeltje houdt het actueel |
| 404-pagina | Craft | `404.html` (kopie van de live 404) |

## Stap 1 — contactformulier activeren (5 min)

1. Ga naar https://web3forms.com, vul het e-mailadres in waar de berichten moeten toekomen
   (bv. hello@ of isabelle@hinnovation.be) en bevestig de mail die je krijgt.
2. Je krijgt een *access key*. Vervang in `contact.html` **en** `en/contact.html` de tekst
   `VUL-HIER-JE-WEB3FORMS-ACCESS-KEY-IN` door die key (of draai `build_static.py` opnieuw met
   `WEB3FORMS_KEY=... python3 build_static.py`).
3. Klaar: de bestaande JavaScript van de site (validatie, succes-/foutmelding) werkt ongewijzigd.

## Stap 2 — hosten (gratis)

**Cloudflare Pages** (aanbevolen, gratis, geen limieten die voor deze site relevant zijn)
1. dash.cloudflare.com → Workers & Pages → Create → Pages → *Upload assets*.
2. Sleep de inhoud van deze map (niet de map zelf) in het venster. Projectnaam bv. `hinnovation`.
3. Je krijgt meteen een preview-URL (`hinnovation.pages.dev`) om alles na te kijken.
4. Custom domain → `www.hinnovation.be` en `hinnovation.be` toevoegen; Cloudflare zegt welke DNS-records je moet zetten.

Alternatief: **Netlify** (netlify.com → *Add new site* → *Deploy manually* → map slepen). Werkt identiek, incl. het `_redirects`-bestand.

De URL's blijven exact gelijk aan vandaag (`/cases`, `/cases/tvh`, `/en/who-we-are`, …): beide hosts
serveren `cases.html` op `/cases`. Google hoeft dus niets te herindexeren.

## Stap 3 — vóór je de oude omgeving opzegt

- **E-mail.** Controleer waar de mailboxen van @hinnovation.be draaien (MX-records van het domein).
  Als die in hetzelfde pakket zitten als de website-hosting, eerst mail verhuizen, dan pas opzeggen.
- **Domeinnaam.** Controleer bij wie hinnovation.be geregistreerd is en of de registratie los staat van de hosting.
- **DNS.** Zet pas de DNS om naar de nieuwe host als de preview-URL volledig goedgekeurd is. Op dat moment wordt
  de oude server onbereikbaar via het domein; opzeggen kan daarna op elk moment.
- Huidige server-IP ter referentie: 185.86.18.57.

## Later iets aanpassen

Alles is gewone HTML. Tekst wijzigen = het `.html`-bestand openen en aanpassen (NL en EN apart), dan de map
opnieuw uploaden. Een nieuwe case toevoegen: kopieer `cases/tvh.html`, pas tekst en beelden aan en voeg een
kaart toe op `cases.html`. Of vraag het aan Claude met deze map als context.

## Bestanden

- `index.html`, `cases.html`, `cases/*.html`, `wie-zijn-we.html`, `contact.html`, `privacy.html`, `cookies.html`, `disclaimer.html`
- `en/…` — dezelfde pagina's in het Engels
- `404.html`, `_redirects`
- `assets/`, `dist/`, `img/`, `favicons/` — beelden, CSS, JavaScript, iconen (ongewijzigd overgenomen)
