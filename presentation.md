---
marp: true
theme: rose-pine
headingDivider: 2
_class: lead
style: |
  img[alt~=center]{
    width: 100%;
    object-fit: contain;
    margin: auto;
    background-color: transparent;
  }
  img[alt~=rounded]{
    margin: auto;
    border-radius: 999px;
  }

  section.resultTable table {
    min-width: 80%;
    margin: 0 auto ;
    font-size: 1.4em;
    white-space: nowrap;
  }
  section.resultTable tr {
    background-color: transparent !important;
    font-weight: 500;
  }
  section.resultTable th {
    font-weight: 900;
  }
  section.resultTable td, section.resultTable th {
    border-color: transparent;
    width: 100%;
  }

  section.resultTable strong {
    color: inherit;
    text-decoration: overline;
  }
  section.resultTable em {
    font-weight: 300;
    font-style: normal;
  }

  section.leftTable table {
    margin-left: 0;
  }

  section.goldTable tr {
    color: var(--gold);
  }
  section.loveTable tr {
    color: var(--love);
  }
  section.roseTable tr {
    color: var(--rose);
  }
  section.foamTable tr {
    color: var(--foam);
  }
  section.irisTable tr {
    color: var(--iris);
  }


  code {
    --color-prettylights-syntax-string: #478dff
  }

  section.centered {
    text-align: center;
  }
  section.centered h1 {
    font-size: 3em;
    font-weight: 700;
  }
---

# Projekt: Optimierung einer VueJS-Web-App

Andreas Nicklaus
Web Performance Optimierung
20.01.2024

[web-performance.andreasnicklaus.de](https://web-performance.andreasnicklaus.de)
![bg](https://v00.leto.andreasnicklaus.de/img/bbblurry.07a8068d.svg)

<!-- Mein Thema:

Optimierung der Webperformance eines VueJS Projekts durch Konfiguration der Vue-Templates und des Build-Prozesses.
 -->

# Agenda

1. Probleme der Webseite
2. Gemachte Änderungen
3. Ergebnisse
4. Was fehlt noch?
![bg](https://v00.leto.andreasnicklaus.de/img/bbblurry.07a8068d.svg)

<!-- 
Um zu zeigen, was ich gemacht habe, habe ich für heute meine Präsentation in 4 Teile unterteilt:

1. Vorstellung der Seite und was damit schlecht oder zumindest verbessungswürdig war
2. 11 Schritte, die ich vorgenommen habe, und was die (nicht) geändert haben
3. Ergebnisse, was rausgekommen ist
4. Ausblick, was noch fehlt
 -->

# Die Webseite

[https://leto.andreasnicklaus.de](https://leto.andreasnicklaus.de)

![h:400 center](img/Homepage.png)

<!-- 
Die Seite, um die es geht, könnt ihr euch nebenbei oder im Anschluss unter leto.andreasnicklaus.de angucken und nutzen.
 -->

# Infos zur Seite

- Marketing-Webseite für Desktopanwendung
- 6 animierte Elemente in der Startansicht
- 2 PNG-Bilder auf der Startseite
- Development:
  - ![h:30](https://upload.wikimedia.org/wikipedia/commons/9/95/Vue.js_Logo_2.svg) VueJS
  - ![h:30](https://avatars.githubusercontent.com/u/22965283?s=280&v=4) Bootstrap-Vue
  - ![h:30](https://cdn.vuetifyjs.com/docs/images/brand-kit/v-logo-circle.svg) Vuetify
- Deployment:
  - ![h:30](https://static-00.iconduck.com/assets.00/aws-ec2-icon-1696x2048-nhw31ife.png) AWS EC2
  - ![h:30](https://www.svgrepo.com/show/353659/docker-icon.svg) Docker
  - ![h:30](https://nginxproxymanager.com/icon.png) Nginx Proxy Manager
  - ![h:30](https://cdn.icon-icons.com/icons2/2699/PNG/512/nginx_logo_icon_169915.png) Nginx

<!-- 
Die Seite, über die ich heute sprechen will, ist eine Marketing-Seite für Leto, eine Anwendung für Pyhsiotherapiepraxen.

Zusätzlich ist eine Nutzerverwaltung und ein Admin-Dashboard für die Anwendung eigebunden.
Die Seite ist also zumindest zum Teil dynamisch.

Startseite: 6 animierte Elemente, 2 große PNGs

Dev: VueJS, Bootstrap-Vue, Vuetify
Deployment: AWS EC2-Instanz, Nginx Proxy Manager, Docker, Nginx
 -->

# Seitenstruktur

- 9 statische & indexierte Seiten
- 3 dynamische & nicht-indexierte Seiten
  - Profilansicht
  - Admin-Dashboard
  - Checkout

<!-- 
9 statische indexierte Seiten
3 dynamische & nicht-indexierte Seiten
 -->

# Probleme der Webseite
![bg](https://v00.leto.andreasnicklaus.de/img/bbblurry.07a8068d.svg)

<!-- Lass uns über die Probleme der Webseite reden -->
---

<!-- _class: resultTable loveTable -->

|                          |          |
| :----------------------- | -------: |
| Time To Interactive      |     4,6s |
| Largest Contentful Paint |     5,2s |
| Lighthouse Performance   |       33 |
| Page Weight              | 2,789 MB |

<!-- Ich habe 4 Indikatoren, wo der Effekt meiner Arbeit am besten merklich ist.

1. Lange TTI
2. Lang ladendes LCP
3. Lighthouse Performance von 33
4. Page Weight von fast 2,8 MB
 -->

---

<!-- _class: resultTable foamTable -->

| Page Weight |       Bytes |
| :---------- | ----------: |
| Bilder      |   2 099 825 |
| JS          |     471 052 |
| CSS         |     221 358 |
| Fonts       |      15 744 |
| HTML        |         515 |
| **Gesamt**  | **~2,7 MB** |

<!-- Beim Page Weight, was ist am am Größten?

1. Bilder 78%
2. Javascript 17,4%
3. CSS 8,2%
4. Fonts 0,5%
5. HTML 0,01%
 -->

# Änderungen 0-3
<!-- _class: resultTable goldTable leftTable -->
| Version | Änderungen                                                        |
| :------ | :---------------------------------------------------------------- |
| Orignal | -                                                                 |
| v01     | Prerendering für statische Seiten                                 |
| v02     | Render-Blocking Stylesheets entfernt <div style="width: 700px;"/> |
| v03     | *Updated Docker Build Workflow*                                   |

<!-- 
Welche Änderungen habe ich also vorgenommen?

Liste an interessanten Änderungen stelle ich im Detail vor, deshalb überspringen wir das!
 -->

# Änderungen 4-7
<!-- _class: resultTable goldTable leftTable -->
| Version | Änderungen                                        |
| :------ | :------------------------------------------------ |
| v04     | *Verbessertes Access Management*                  |
| v05     | AVIF-Bilder, Chained Request für Fonts entfernt   |
| v06     | Lineare Verteilung der Bildgrößen                 |
| v07     | Import nur der genutzten Icons anstelle von allen |

# Änderungen 8-11
<!-- _class: resultTable goldTable leftTable -->
| Version | Änderungen                                                  |
| :------ | :---------------------------------------------------------- |
| v08     | JS-Chunks gesplittet                                        |
| v09     | Animationen entfernt                                        |
| v10     | Alle Bilder werden lazy-loaded <div style="width: 700px;"/> |
| v11     | Zuerst sichtbare SVGs werden lazy-loaded                    |

# v01: Prerendering

```js
new PrerenderSpaPlugin({
  staticDir: path.join(__dirname, 'dist'),
  routes: routes.filter(r => r.meta?.prerender).map(r => r.path),
  renderer: new PrerenderSpaPlugin.PuppeteerRenderer({
    inject: {},
    renderAfterElementExists: '[data-view]',
  }),
  postProcess: (renderedRoute) => {
    renderedRoute.html = renderedRoute.html
      .replace(/<script (.*?)>/g, '<script $1 defer>')
      .replace('id="app"', 'id="app" data-server-rendered="true"');

      return renderedRoute;
    }
  })
```

<!-- 
Erster Schritt:

Im Build-Prozess mit dem PrerenderSpaPlugin, weil Vue mit einem HTML-Skelett arbeitet und es nach dem Laden des JS füllt.

- nur die statischen Seiten
- gut für den Index
- zusätzlich werden alle Skripte mit den "defer" versehen, damit es dem Rendering des jetzt vorhandenen vollständigen HTML.
 -->

# v01: Prerendering

<!-- _class: resultTable loveTable -->

|                          | Original |     v01 |
| :----------------------- | -------: | ------: |
| Time To Interactive      |     4,6s | *14,5s* |
| Largest Contentful Paint |   *5,2s* |    3,3s |
| First Contentful Paint   |   *4,6s* |    3,3s |
| Lighthouse Performance   |     *33* |      57 |

<!-- 
Der Effekt des Prerendering ist gleich erkennbar.

- Die TTI verdreifacht sich auf fast 15 Sekunden, weil es einfach mehr zu Laden und animieren gibt
- LCP wird schneller geladen, weil das HTML zum Laden der Bilder früher da ist
- FCP genauso
- aus diesen 2 Gründen: Performance 57
 -->

# v02: Renderblocking-Stylesheets entfernt

```js
postProcess: (renderedRoute) => {
  renderedRoute.html = renderedRoute.html
    .replace(
      /<link href="(.*?)" rel="stylesheet">/g,
      `<link rel="preload" href="$1" as="style" onload="this.onload=null;this.rel='stylesheet'">
      <noscript>
        <link rel="stylesheet" href="$1">
      </noscript>`
    )
    .replace(
      /<link rel="stylesheet" (.*?)>/g,
      `<link rel="preload" $1 as="style" onload="this.onload=null;this.rel='stylesheet'">
      <noscript>
        <link rel="stylesheet" $1>
      </noscript>`
    )
    .replace(/<script (.*?)>/g, '<script $1 defer>')
    .replace('id="app"', 'id="app" data-server-rendered="true"');

    return renderedRoute;
  }
```

<!-- 
Im Zweiten Schritt habe ich versucht, Render-Blocking CSS automatisiert zu entfernen:

Prerendering-Plugin erweitern durch replace-Funktionen
Durch Vue-Plugins 2 Versionen, Stylesheets einzubinden
1. link-href-rel
2. link-rel-href

Wird zu
<link> mit rel=preload, durch js rel=stylesheet
<noscript>
<link rel=stylesheet>
</noscript>
 -->

# v02: Renderblocking-Stylesheets entfernt

<!-- _class: resultTable loveTable -->
|                          | Original |     v01 |     v02 |
| :----------------------- | -------: | ------: | ------: |
| Time To Interactive      |     4,6s | *14,5s* | *10,4s* |
| First Contentful Paint   |   *4,6s* |  *3,3s* |    0,9s |
| Largest Contentful Paint |   *5,2s* |  *3,3s* |    2,6s |
| Lighthouse Performance   |     *33* |      57 |    *45* |

<!-- 
Was hat das gebracht?

- TTI zum 4 Sekunden verbessert
- FCP um 2,4 Sekunden, über 70% verbessert
- LCP um 0,7 Sekunden verbessert, jetzt 50% des Originals
- Lighthouse Performance von 57 auf 45 runter, k.A. wieso
 -->

# v05: Chained Request für Fonts entfernt

Bevor in `App.vue`:
```html
<style lang="scss">
  @import url("https://fonts.googleapis.com/css2?family=Roboto&display=swap");
</style>
```

Danach in `index.html`:
```html
<link
  rel="stylesheet"
  href="https://fonts.googleapis.com/css2?family=Roboto&display=swap"
/>
```

<!-- 
[v05 Teil 1]
v03 und v04 waren nicht zur Performanceoptimierung, deshalb v05: Chained Requests für Fonts

Link zur Font in index.html anstelle vom Verweis im style-Block in App.vue
 -->

# v05: AVIF-Bilder (alt)

```html
<img
  :src="appleDevices"
  :srcset="`${appleDevices_webp_1} 200w, ${appleDevices_webp_2} 783w,
  ${appleDevices_webp_3} 1123w, ${appleDevices_webp} 1920w`"
  sizes="(max-width: 768px) 100vw, 50vw"
/>
```

<!--
[v05 Teil 2]
PNG zu AVIF-Format

Außerdem in v05 habe ich die Einbindung von Bildern auf der Seite getauscht. Was vorher wie hier ein Image-Tag mit einem Srcset auf Webp-Bilder war,...
 -->

# v05: AVIF-Bilder (neu)

```html
<picture>
  <source
    :srcset="`${appleDevices_avif_1} 200w, ${appleDevices_avif_2} 783w,
      ${appleDevices_avif_3} 1123w, ${appleDevices_avif} 1920w`"
    sizes="(max-width: 768px) 100vw, 50vw"
  />
  <source
    :srcset="`${appleDevices_webp_1} 200w, ${appleDevices_webp_2} 783w,
      ${appleDevices_webp_3} 1123w, ${appleDevices_webp} 1920w`"
    sizes="(max-width: 768px) 100vw, 50vw"
  />
  <img :src="appleDevices_webp" ... />
</picture>
```
<!-- 
...ist jetzt ein Picture-Tag mit 2 Source-Tags:

1. für AVIF-Bilder
2. für Webp-Bilder

mit den gleichen Größen.
 -->

# v05: Format Beispiel

- PNG: **611 kB** 
(nicht verwendet)
- WEBP:
  - **126 kB** (Original)
  - **112 kB** (klein)
- AVIF:
  - **374 kB** (Original)
  - **48 kB** (klein)

![bg right:60%](img/mockup-coffee-macbook.avif)

<!-- 
Für die Conversion vom Originalbild in PNG habe ich das NPM-Package `sharp` benutzt und eine kleine Entdeckung für mich gemacht

1. Im Webp-Format ist das Bild in der gleichen Größe knapp ein Sechstel groß, aber die nächstkleinere Größe ist maginal kleiner
2. Im AVIF-Format ist das Bild in Originalgröße nur knapp halb so groß, aber die nächstkleinere Größe ist etwa ein Neuntel vom Orignalgroßen AVIF.

Rechts das Bild, von dem die Daten kommen.
 -->

# v05: Format Beispiel

<!-- _class: resultTable loveTable -->

|                         |   Original |        v04 |      v05 |
| :---------------------- | ---------: | ---------: | -------: |
| Time To Interactive     |       4,6s |    *13,3s* |   *6,1s* |
| Speed Index             |     *7,5s* |     *4,1s* |     2,5s |
| Page Weight             | *2,789 MB* | *2,738 MB* | 1,140 MB |
| Cumulative Layout Shift |      0,751 |    *0,936* |  *0,780* |

<!-- 
Was hat das gebracht?

- TTI wieder auf einen semi-akzeptablen Wert von 6,1 Sekunden zurückgebracht
- SI um 1,5 Sekunden verbessert auf neuen Bestwert von 2,5 Sekunden
- Page Weigth um fast 60% reduziert -> Bilder
- CLS wieder auf Orignalwert zurückgebracht -> Image Sizes
 -->

# v06: Lineare Verteilung der Bildgrößen

vorher:
```html
<source
  :srcset="`${appleDevices_avif} 1920w, ${appleDevices_avif_3} 1123w,
  ${appleDevices_avif_2} 783w, ${appleDevices_avif_1} 200w`"
  sizes="(max-width: 768px) 100vw, 41.67vw"
/>
```
nachher:
```html
<source
  :srcset="`${appleDevices_avif} 1920w, ${appleDevices_avif_1} 1600w,
  ${appleDevices_avif_2} 1280w, ${appleDevices_avif_3} 960w,
  ${appleDevices_avif_4} 640w, ${appleDevices_avif_5} 320w`"
  sizes="(max-width: 768px) 100vw, 41.67vw"
/>
```

<!-- 
In Version 6 habe ich die Schrittweite zwischen den Bildgrößen geändert

von 4 Bildern
auf 6 Bildern mit gleicher Schrittweite
 -->

# v07: Import nur der genutzten Icons

```js
import { BootstrapVueIcons } from 'bootstrap-vue'
Vue.use(BootstrapVueIcons)
```
```js
import { BootstrapVue, BIconBoxArrowUpRight, BIconPerson, ... } from 'bootstrap-vue'

Vue.component("b-icon-box-arrow-up-right", BIconBoxArrowUpRight)
Vue.component("b-icon-person", BIconPerson)
...

```

<!-- 
Genug von Bildern!

In Version 7 und 8 habe ich den JS-Dateien angenommen.

Als erstes ist mir aufgefallen, dass ein Großteil der JS-Module von Bootstrap-Icons eingenommen wurde, weil ich sie alle importiere.

Also habe ich nur die genutzten Icons importiert und als Vue-Componenten registriert.
 -->

# v08: JS-Chunks gesplittet

```js
configureWebpack: (config) => {
  config.optimization = {
    runtimeChunk: 'single',
    splitChunks: {
      chunks: 'all',
      maxInitialRequests: Infinity,
      maxSize: 500_000,
    }
  }
}
```

<!-- 
In v08 habe ich zusätzlich mit den JS-Chunks rumgespielt und mit den Built-In Optionen von Webpack die Größe der Dateien begrenzt.

Motivation dafür war, dass die als erstes geladenen JS-Datei sehr groß war und vieles davon nicht auf der Startseite genutzt wird.
 -->

# v08: JS-Chunks gesplittet

<!-- _class: resultTable loveTable -->


|                      |       v06 |     v07 |      v08 |
| :------------------- | --------: | ------: | -------: |
| Anzahl JS-Dateien    |      *30* |    *30* |       62 |
| Raw Größe JS-Dateien | *5,75 MB* | 4,95 MB |  4,95 MB |
| Page Weight          |  *778 kB* |  612 kB | *628 kB* |

<!-- 
Was hats gebracht?

- Anzahl und damit Granulatität an JS-Dateien verdoppelt
- Durch Bootstrap Icons ca. 14% raw eingepart
- Durch Bootstrap Icons ca. 21% gzipped eingepart
 -->

# v09: Animationen entfernt

mit Animationen (um 1100ms verzögert)

```html
<div
  data-aos="fade-up"
  data-aos-delay="1100"
  data-aos-anchor-placement="bottom"
>
  <b-button><b-icon-arrow-down variant="primary"/></b-button>
</div>
```
ohne Animationen:

```html
<div>
  <b-button><b-icon-arrow-down variant="primary"/></b-button>
</div>
```

<!-- 
Animationen im Filmstrip als Visual Change vorhanden.
Max 1100ms Verzügerung bis Start.

Keine Änderung in sonstigen Metriken.
 -->

# Alle Bilder (v10) & SVGs (v11) werden lazy-loaded
v10:
```html
<picture>
  <source .../>
  <source .../>
  <img
    ...
    loading="lazy"
  />
</picture>
```
v11:
```html
<img
  ...
  loading="lazy"
/>
```

<!-- 
Formal gefehlt hats noch gefehlt, dass Bilder Lazy-Loaded geladen werden, deswegen habe ich das noch in Version 10 hinzugefügt und ...
in Version 11 habe ich das noch für SVGs gemacht.
 -->

# v10 & v11: Lazy-loading

<!-- _class: resultTable loveTable -->

|                          |    v09 |    v10 |  v11 |
| :----------------------- | -----: | -----: | ---: |
| Lighthouse Performance   |     54 |   *44* |   54 |
| Speed Index              | *2,6s* | *3,9s* | 2,5s |
| Largest Contentful Paint | *2,7s* | *4,1s* | 2,6s |

<!-- 
Was hat es gebracht?

Aus irgendeinem Grund, hat das Lazy-Loading von Bildern sowohl die Lighthouse Performance als auch Speed Index und LCP verschlechtert, was sich durch das Lazy-Loading von SVGs wieder ausgebessert hat.

Wenn also jemand eine Vermutung hat, woran das gelegen hat, bitte ich herzlich um Hilfe.
 -->

# Ergebnisse - Visualisierungen
![bg](https://v00.leto.andreasnicklaus.de/img/bbblurry.07a8068d.svg)

<!-- 
Ich habe die Metriken und Ergebnisse noch visualisiert, damit die Verbesserungen und Verschlechterungen besser sichtbar werden.
 -->

---
<!-- _class: resultTable irisTable -->

| Lighthouse Performance | Score |
| :--------------------- | ----: |
| Original               |    33 |
| v01: Prerendering      |    57 |
| v11: Lazy-Loading      |    54 |
<!-- Zuerst zur Lighthouse Performance, die ich erst von 33 auf 57 durch Prerendering gehoben habe.
Bis heute ist der Score bei 54. -->
---
![center](https://quickchart.io/chart?c={type:"line",data:{labels:['v00','v01','v02','v03','v04','v05','v06','v07','v08','v09','v10','v11'],datasets:[{label:"Lighthouse%20Performance%20Score",data:[33,57,45,40,46,51,49,52,54,54,44,54],backgroundColor:"%23c4a7e755",borderColor:"%23c4a7e7"}]},options:{scales:{xAxes:[{scaleLabel:{display:true,labelString:'Version'}}],yAxes:[{scaleLabel:{display:true,labelString:'Score'}}]}}})
<!-- Hier sehen wir, wie sehr der Score geschwankt hat -->
---
<!-- _class: resultTable goldTable -->

| Time To Interactive     | Score |
| :---------------------- | ----: |
| Original                |  4,6s |
| v10: lazy-loaded Images |  3,9s |
<!-- Die Time-To-Interactive habe ich runtergebracht von 4,6s auf 3,9s -->
---
![center](https://quickchart.io/chart?c={type:"line",data:{labels:['v00','v01','v02','v03','v04','v05','v06','v07','v08','v09','v10','v11'],datasets:[{label:"Time%20To%20Interactive",data:[4.6,14.5,10.4,14.7,13.3,6.1,4.9,3.9,4.1,4.1,3.9,4],backgroundColor:"%23e9b77277",borderColor:"%23e9b772"}]},options:{scales:{xAxes:[{scaleLabel:{display:true,labelString:'Version'}}],yAxes:[{scaleLabel:{display:true,labelString:'Sekunden'},ticks:{min:0}}]}}})
<!-- Und hier können wir nochmal begutachten, dass im Laufe des Projekts durch Prerendering die TTI erst hochgegangen und dann durch die Umstellung auf AVIF-Bilder in Version 5 wieder runtergegangen ist. -->
---
<!-- _class: resultTable roseTable -->

| Largest Contentful Paint    | Score |
| :-------------------------- | ----: |
| Original                    |  5,2s |
| v05: AVIF, Chained Requests |  2,5s |
| v11: lazy-loaded SVGs       |  2,6s |
<!-- Dann kommen wir jetzt zu den Kriterien, die sich tatsächlich verbessert haben.

Den LCP habe ich halbieren können, aber... -->
---
![center](https://quickchart.io/chart?c={type:"line",data:{labels:['v00','v01','v02','v03','v04','v05','v06','v07','v08','v09','v10','v11'],datasets:[{label:"Largest%20Contentful%20Paint",data:[5.2,3.3,2.6,2.3,2.4,2.5,2.5,2.5,2.5,2.7,4.1,2.6],backgroundColor:"%23ebbcba55",borderColor:"%23ebbcba"}]},options:{scales:{xAxes:[{scaleLabel:{display:true,labelString:'Version'}}],yAxes:[{scaleLabel:{display:true,labelString:'Sekunden'},ticks:{min:0}}]}}})
<!-- wie eben angesprochen, gibt es einen Auschlag durch Lazy-Loading, den ich nicht erklären kann. -->
---

<!-- _class: resultTable foamTable -->

| Page Weight                          |      Bytes |
| :----------------------------------- | ---------: |
| Original                             |    2789 kB |
| v05: Bilder im AVIF-Format           |   -1649 kB |
| v06: lineare Bilder-Größenverteilung |    -362 kB |
| v07: Importiere nur genutzte Icons   |    -166 kB |
| **Gesamt**                           | **612 kB** |
<!-- Zu guter Letzt das Page Weight habe ich reduziert bekommen von 2789 kB auf 612kB.

Das ist passiert in den Versionen 5, 6 und 7 durch Reduzierung der Bildgröße und importierten Icons. -->
---
![center](https://quickchart.io/chart?c={type:"line",data:{labels:['v00','v01','v02','v03','v04','v05','v06','v07','v08','v09','v10','v11'],datasets:[{label:"Page%20Weight",data:[2789,2737,2780,2737,2738,1140,778,615,628,627,628,627],backgroundColor:"%239ccfd855",borderColor:"%239ccfd8"}]},options:{scales:{xAxes:[{scaleLabel:{display:true,labelString:'Version'}}],yAxes:[{scaleLabel:{display:true,labelString:'kB'},ticks:{min:0}}]}}})
<!-- Das kann man an dem Graphen, dass die Versionen 5-7 tatsächlich effektiv waren und die Größe deutlich verbessert haben. -->
# Was fehlt noch?

Nach dem Lighthouse Performance Report:
- CSS Pruning
- Automatisiertes Treeshaking
- "Minimize main thread work"
- Preloading LCP-Bild
- Effizienteres Caching mit CDN

Nach Image Linter:
- Größere Bildversionen für große Bildschirme

<!-- Jetzt, wo wir gesehen haben, was ich gemacht und erreicht habe, können wir nochmal einen kurzen Ausblick drauf werfen, was ich noch machen sollte.

Nach dem Lighthouse Performance Report fehlt noch:

1. CSS Pruning, dass ungenutztes CSS entfernt wird. Das habe ich bisher nicht zum Laufen bekommen.
2. Da das Entfernen von Bootstrap-Icons so effektiv war, sollte Treeshaking auch noch automatisiert werden.
3. Thread Work ist laut Performance Report auch sehr groß. Ich habe bisher noch keinen Anhaltspunkt, wie ich anfange.
4. Das LCP-Bild dauert noch lange zu laden, deshalb sollte das Bild Preloaded werden, aber es ist größenabhängig, deshalb gehört da noch mehr Überlegung dazu.
5. Außerdem durch den Nginx Proxy Manager nicht sonderlich effektiv gehandelt: Caching. Mittels einem CDN, könnte das sehr verbessert werden.

Nach dem Image Linter, den ich verwendet habe:
1. Von Hochkant-Bildern fehlen Bilder in großen Bildschirmgrößen

-> Effektives Vergrößern von Bildern ohne höheren Datenaufwand
 -->
# Das wars!
<!-- _class: centered -->
Versions-URLs: [vXX.leto.andreasnicklaus.de](https://v00.leto.andreasnicklaus.de)

![bg](https://v00.leto.andreasnicklaus.de/img/bbblurry.07a8068d.svg)

---

<!-- class: resultTable goldTable -->
![bg](https://v00.leto.andreasnicklaus.de/img/bbblurry.07a8068d.svg)


|                                                                                                                                             | Andreas Nicklaus   <br>   ![h:200 rounded](https://media.licdn.com/dms/image/C5603AQGSV-yyfbgmeg/profile-displayphoto-shrink_200_200/0/1623311887654?e=1709769600&v=beta&t=qPack9A-o02XTnsWjvev62PBJEjEiMXSUscabd7qR_o) |                                                                                  |
| :-----------------------------------------------------------------------------------------------------------------------------------------: | :---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------: | :------------------------------------------------------------------------------: |
|                                                                                                                                             |                                                                                                                                                                                                                         |                                                                                  |
| [![h:40](https://upload.wikimedia.org/wikipedia/commons/9/96/Instagram.svg)<br>@andreasnicklaus](https://www.instagram.com/andreasnicklaus) |                                    [![h:40](https://upload.wikimedia.org/wikipedia/commons/8/81/LinkedIn_icon.svg)<br>andreasnicklaus](https://www.linkedin.com/in/andreasnicklaus/)                                    | [![h:40](img/Web.svg)<br>andreasnicklaus.de](https://www.www.andreasnicklaus.de) |