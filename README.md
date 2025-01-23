# Guide: Kom igång med Node.js och Express för backend
Att bygga en backend behöver inte vara så svårt som man kan tro, vi ska titta på hur man ta sig an detta med hjälp av node.js och Express!
Sedan kommer vi bygga vidare med att använda mongodb som databas!
## Förutsättningar
- Grundläggande kunskaper i JavaScript.
- Kunskap om React.js (t.ex. komponenter, state, props, fetch API).
- Installerad Node.js (https://nodejs.org).
- Visual Studio Code

## 1. Vad är Node.js och Express?
- Node.js: En JavaScript-runtime som körs utanför webbläsaren. Perfekt för att bygga serverapplikationer.
- Express: Ett minimalt och flexibelt ramverk för att bygga webbapplikationer och API:er med Node.js.

## 2. Projektstruktur
Vi vill separera front end (React) och backend (Node.js/Express), så en typisk struktur kan se ut så här:

```
my-project/
├── client/      (React-projektet)
├── server/      (Node.js/Express-backend)
├── package.json (Hanterar båda delarna i projektet)
```
## 3. Skapa Back-end projektet

Öppna ett react projekt, skapa en mapp där i som heter server, så att strukturen i mapparna ser ut som beskrivet ovan.
I terminalen som finns i VS code går du in i mappen du skapat.
```
cd server
```
Sedan så "Initierar" vi ett node.js projekt:
```
npm init -y
```
Sedan ska vi installera några saker som kommer behövas, fortsätt i samma terminal:
```
npm install express
npm install body parser
npm install cors
```
Vad är detta då? Jo,  kort:
- Express: Bygger servern.
- body-parser: Hanterar JSON-data från klienten.
- cors: Tillåter kommunikation mellan React och backend under utveckling.

## 4. Bygg Backend servern

1. Skapa en fil i mappen server som heter `server.js`
2. Öppna sedan filen och skriv följande:

```
const express = require('express');
const bodyParser = require('body-parser');
const cors = require('cors');

const app = express();
const PORT = 5000;

// Middleware
app.use(bodyParser.json());
app.use(cors());

// En test-route
app.get('/api', (req, res) => {
    res.json({ message: 'Hello from Express!' });
});

// Starta servern
app.listen(PORT, () => {
    console.log(`Backend server running at http://localhost:${PORT}`);
});
```
3. Starta servern
I samma terminal som innan, skriv:
```
node server.js
```
Detta är som att skriva `npm run dev`, fast för servern/backend. Så nu kan du prova gå in på `http://localhost:5000/api` I Safari eller Edge, och detta borde visas där:
```
{ "message": "Hello from Express!" }
```
Så! Med detta så har du det minsta som behövs för att man ska kunna kalla det för en backend, det är drygt att sätta upp projekt i början, och det är inte där man ska lägga sin tid egentligen.
Om vi ska bygga vidare på detta så borde du tänka; Vad är det som får detta att funka egentligen? Vad är det för kod som egentligen körs när jag går till `http://localhost:5000/api` ?

Jo, vi har lagt till en "route" i `server.js` i koden ser det ut så här:
```
app.get('/api', (req, res) => {
    res.json({ message: 'Hello from Express!' });
});
```
I ovan kod så säger vi till `app` att vi vill lyssna på när någon i webläsaren försöker prata med `/api`
Och när någon gjort det så skickar vi ett javascript object som svar!
```
{ message: 'Hello from Express!' }
```
`res` i det här fallet står för response, allså svar, och vi vill svara med Json.
Så vi använder oss av variabeln `res` och anropar metoden `json` och "ger den metoden" vårat objekt, alltså:
```
res.json({ message: 'Hello from Express!' });
```
Kan du nu lägga till en egen
