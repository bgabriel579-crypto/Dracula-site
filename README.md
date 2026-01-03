# Dracula-site — Site static profesional cu Web3 și i18n

Aceasta versiune include integrare Web3 (conectare wallet, citire sold BNB & token, adăugare token în wallet, comutare rețea BSC), integrare cu DexScreener pentru feed de preț (când API-ul este disponibil), link direct la PancakeSwap și suport multilingv (Română, English, 中文, Français, Español).

Fișiere incluse:
- `index.html` — pagina principală cu UI i18n și butoane Web3
- `styles.css` — stiluri responsive dark
- `script.js` — logica Web3, DexScreener, i18n
- `logo.svg` — (adaugă-ți un logo SVG în rădăcina)

Setări rapide / instrucțiuni:
1. Copiază fișierele în root-ul site-ului (sau în folder `docs/` dacă folosești GitHub Pages).
2. Deschide `index.html` în browser. Pentru funcționalități Web3 complete folosește un browser cu MetaMask sau alt wallet injectat.
3. Butoane cheie:
   - Connect: conectează wallet-ul (MetaMask). Scriptul încearcă să comute rețeaua la BSC (56) dacă nu e setată.
   - Add token: înceracă `wallet_watchAsset` pentru a adăuga tokenul DRAC în wallet.
   - Copy contract: copiază adresa contractului în clipboard.
   - View on DexScreener: deschide pagina de pereche DexScreener (live).
   - Buy on PancakeSwap: deschide pagina PancakeSwap cu tokenul preselectat.

Despre feed-ul de preț:
- Scriptul încearcă mai întâi DexScreener (public API: `https://api.dexscreener.com/latest/dex/tokens/bsc/<token>`).
- Din cauza CORS sau dacă tokenul nu are date pe DexScreener, scriptul revine la o valoare simulată. Poți înlocui / extinde `updateStatsLoop()` în `script.js` pentru a folosi un backend sau CoinGecko (dacă tokenul este înregistrat acolo).
- Recomandare: folosește un mic backend (lambda / cloud function) pentru a face proxy la DexScreener/CoinGecko și a evita problemele CORS și limitări.

Securitate & permisiuni:
- `wallet_watchAsset` depinde de suportul wallet-ului (MetaMask oferă).
- `wallet_switchEthereumChain` / `wallet_addEthereumChain` sunt metode standard; utilizatorul poate refuza.
- Nu trimitem tranzacții direct din site; pentru cumpărare redirectăm utilizatorul la PancakeSwap. Dacă dorești funcționalitate on-site (approve/swap) pot adăuga butoane care lansează tranzacții (cu confirmare wallet).

Îmbunătățiri posibile (pot implementa):
- Integrare WalletConnect (mobile), Web3Modal (pentru mai multe wallet-uri).
- Interfață de swap directă (creare tx către PancakeSwap Router).
- Backend pentru agregare statistici, calcul marketcap real, holders count (folosind BscScan APIs).
- Pagini adiționale: Whitepaper, Tokenomics detaliat, Team, Press kit.
- Localizare detalii: formate nume/date conform localizării.

Vrei să continui cu:
- Adăugare WalletConnect / Web3Modal?
- Adăugare proxy backend pentru DexScreener/CoinGecko (pot oferi un exemplu AWS Lambda / Netlify Function)?
- Implementare swap direct (approve + swap) — atenție: necesită testare și confirmări de securitate.

Am inclus fișierele la root. Testează local și spune-mi dacă vrei să adaug WalletConnect sau un backend proxy.
