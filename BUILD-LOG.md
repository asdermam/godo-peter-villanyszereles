# Godó Péter villanyszerelés — build log

Demó weboldal a workflow (AI WORKFLOW vault) szerint. Lead #6.

## Step 1 — Kontextus
- **Cég:** Godó Péter villanyszerelés — egyéni vállalkozó, villanyszerelő
- **Cím:** 2113 Erdőkertes, Béke u. 44. · **GPS:** 47.6637409, 19.316827
- **Tel:** +36 20 807 7769 · **E-mail:** petergodo@gmail.com · **Facebook:** van oldala
- **Szolgáltatások:** teljes körű villanyszerelés magánszemélyeknek és cégeknek; új elektromos hálózat kiépítése, meglévő bővítése vagy cseréje; hibakeresés és javítás; villanybojler tisztítása, javítása és cseréje
- Forrás: https://kertesivallalkozasok.hu/item/godo-peter-villanyszereles/

## Step 2 — ChatGPT prompt + dizájn kutatás (ÚJ chat a leadhez)
ChatGPT (browser, új chat) tartalmi/strukturális terve (csak a TARTALOMHOZ; kódot/vizuált Claude készít).

ChatGPT prompt (amit megadtam):
> „Egy magyar nyelvű, eladásra szánt demó landing weboldalt építek egy helyi villanyszerelő vállalkozásnak. Céged: „Godó Péter villanyszerelés" — egyéni vállalkozó, Erdőkertes … Kérlek készíts egy RÉSZLETES TARTALMI és STRUKTURÁLIS tervet ehhez a weboldalhoz: szekciók sorrendje, tartalma, javasolt magyar szövegek/címsorok/CTA-k, hangnem, SEO kulcsszavak. FONTOS: csak a TARTALOMRA koncentrálj — a vizuális dizájnt és a kódot én készítem, NE adj konkrét kód- vagy CSS/dizájn megoldásokat."

ChatGPT javasolt szerkezete: Fejléc (kiemelt tel + „Hívás most") → Hero (H1: „Megbízható villanyszerelés Erdőkertesen és környékén", bizalmi pontok) → Probléma („Villanyszerelési problémája van?…") → Szolgáltatások → Villanybojler (külön kiemelt) → Miért érdemes minket hívni → Folyamat → Szolgáltatási terület → GYIK → Kapcsolat. Hangnem: helyi, szakemberes, bizalomkeltő, túlígérgetés nélkül (NEM „24/7", NEM „azonnali kiszállás"). Fő CTA: telefonhívás. SEO: „villanyszerelő Erdőkertes", „hibakeresés", „hálózatépítés", „villanybojler".

**Választott dizájn irány (Claude sajátja, NEM ChatGPT-től):** sötét „elektromos éjszaka" téma — mély éjkék (#080D1A) alap, borostyán-sárga (amber #FFB224) villám akcent, elektromos cián (#35C8F0); finom áramköri (circuit) rács és animált trace-vonalak, SVG „chip + villám" hero-illusztráció. Betűk: Space Grotesk (display) + Instrument Sans (body) + Spline Sans Mono (technikai/label). Cél: megkülönböztethető, nem generikus megjelenés (az előző 5 demótól is eltérő).

## Step 2 — Logó (ChatGPT kép-generálás, ugyanabban a chatben)
Egy generálásra megfelelő lett: kör alakú embléma — sötétkék körkontúr, bal oldalon dugvilla (plug) motívum, középen erős borostyán-sárga villám, fehér háttéren. Pontosan illik a témához (kék + amber). 256×256-ra kicsinyítve (canvas), base64-ként a Vite `assetsInlineLimit` felhúzásával a build egyfájlos HTML-jébe került. Fejlécben és footerben `rounded-xl` badge-ként, cián ring-gel.

## Step 3 — Build & test
**Build:** Vite 6 + React 18 + Tailwind v4, `vite-plugin-singlefile` → egy `dist/index.html` (~334 kB, minden inline).
Szekciók: Header (sticky + mobil drawer) · Hero (circuit SVG + villám chip) · Bizalmi sáv · Probléma · Szolgáltatások (4 kártya) · Villanybojler (kiemelt) · Rólunk / Miért érdemes hívni · Folyamat (4 lépés) · Szolgáltatási terület (Erdőkertes + környék) · GYIK (React accordion) · Kapcsolat (tel/email/**Cím→Google Maps**/Facebook + demó űrlap) · Footer.

**Tesztelés (Playwright MCP):**
- Console: 0 hiba, 0 figyelmeztetés (dev és a bundle-ölt dist verzión is).
- Reszponzivitás: 390 (mobil) és 1440 (desktop) — layout minden töréspontnál rendben, tartalom hiánytalan.
- Interakciók: GYIK accordion nyit/zár (csak egy panel nyílik egyszerre) ✓ ; mobil menü nyílik/záródik, 6 link + „Hívás most" ✓.
- Linkek: 9× `tel:+36208077769`, 3× `mailto`, 3× **Cím → Google Maps** (GPS koordinátával, új lap), 1× Facebook ✓. Logó base64-ként betölt a bundle-ben ✓.
- A „Cím → Google Maps" a korábbi hiba (vault Mistakes) tanulsága alapján eleve beépítve; minden elérhetőség kattintható.

## Step 4/5 — Publikálás & hidegemail
- Publikálva GitHub Pages-re a `gh` CLI-vel: https://asdermam.github.io/godo-peter-villanyszereles/
- Hidegemail (Step 5): emberi jóváhagyásra vár, még NEM ment ki.
