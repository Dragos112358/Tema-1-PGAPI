#  Oldie Room (OpenGL)

Acest proiect este o simulare 3D interactivă dezvoltată în C++ și OpenGL. Scena prezintă o cameră detaliată, generată procedural, care include elemente de mobilier, un televizor funcțional, lumini dinamice, sisteme de particule și fizică de bază (coliziuni). Utilizatorul poate interacționa cu mediul înconjurător folosind arme (o bâtă de baseball și un pistol) pentru a distruge obiecte, poate modifica setările de iluminare și poate schimba tematica vizuală a întregii scene.

---

## Funcționalități Principale & Bonusuri Implementate

* **Generare Procedurală (Geometrie):** Formele obiectelor (vaze, picioare de scaune/mese, lămpi, sticle) sunt generate matematic folosind curbe Bezier, suprafețe de rotație și translație.
* **Reflexii Dinamice (Cubemapping):** Sticlele, paharele și ecranul televizorului reflectă mediul înconjurător în timp real.
* **Sistem de Particule:** Artificii animate vizibile atât pe ecranul TV-ului, cât și reflectate pe suprafețele de sticlă.
* **Umbre (Shadow Mapping):** Scena folosește un Framebuffer dedicat pentru a genera umbre realiste în funcție de sursa de lumină.
* **Iluminare Avansată:** Sursă de lumină (lampa) controlabilă (poziție, direcție, intensitate, culoare). Include efect de *flickering/lightning* (stroboscop).
* **Interacțiune & Coliziuni:** Jucătorul poate folosi o bâtă de baseball sau un pistol pentru a distruge obiecte (Pringles, vaze, sticle). Sistemul folosește coliziuni avansate (Segment-Segment și Rază-Sferă/Capsulă).
* **Sistem de Theming:** Posibilitatea de a schimba texturile întregii lumi printr-o singură apăsare de buton (2 scenarii complet diferite).

---

## Controale și Interacțiune

### Control Lumini
* `W` / `A` / `S` / `D` / `Q` / `E` - Deplasează lampa și sursa de lumină prin scenă.
* `U`, `I`, `O`, `J`, `K`, `L` - Rotește direcția luminii.
* `5` / `6` - Scade / Crește intensitatea luminii.
* `R` / `G` / `B` - Crește componenta de culoare (Roșu, Verde, Albastru) a luminii.
* `Shift` + `R/G/B` - Scade componenta de culoare a luminii.
* `F` - Activează/Dezactivează efectul de *Flickering* (fulgere/stroboscop).

### Interacțiune și Arme
* `7` - Echipează / Dezechipează Bâta de baseball.
* `8` - Echipează / Dezechipează Pistolul.
* `N` - Acțiune: Lovește cu bâta (Swing) / Trage cu pistolul (Shoot).
* `Z` - Undo: Reface ultimul obiect distrus.

### Control Mediu & Cameră
* `1` / `2` - Rotește televizorul.
* `3` - Comută între modul de vizualizare Solid (Fill) și Wireframe (Lines).
* `4` - Ascunde / Arată obiectele dinamice din scenă.
* `9` - Schimbă tematica texturilor (Scenariul 1 vs. Scenariul 2).
* `P` - Comută complexitatea geometriei (High-Poly vs. Low-Poly pentru vaze și mobilier).
* `T` - **Reset complet al scenei** (aduce toate obiectele și luminile la starea inițială).

---

## Detalii Tehnice

1. **Custom Framebuffers (FBO):** Proiectul folosește multiple FBO-uri pentru a randa umbrele (Depth Map), reflexiile camerei (Cubemap principal de 512x512) și reflexiile specifice sticlelor (Cubemaps secundare de 256x256 pentru optimizare).
2. **Shadere Personalizate:** Logica de generare a suprafețelor se face direct în GPU, folosind `GeometryShader` pentru instanțiere și extrudare.
3. **Optimizare:** Utilizarea `glDrawElementsInstanced` pentru a desena eficient zeci de obiecte complexe fără a aglomera CPU-ul, și Culling dinamic (Backface/Frontface) adaptat în funcție de obiectul randat.
