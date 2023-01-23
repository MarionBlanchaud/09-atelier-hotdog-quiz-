# HotDog Quiz

![HotDog Quiz](https://user-images.githubusercontent.com/87300647/184116181-63240166-9fa4-432d-bb7c-9bdd71af71ea.png)

Nous avons décidé d'organiser un HotDog Quiz au sein d'O'Clock (c'est un peu comme le BurgerQuiz mais en différent) et nous avons besoin d'un système simple pour compter les points des deux équipes : "Ketchup" et la team "Moutarde".

<small>*Toute resemblance avec le BurgerQuiz d'Alain Chabat n'est que pure coincidence... Bien évidement 😉*</small>

## Énoncé débrouillard

Installer SASS.

Sans créer d'autres pages ni de composants au sein du `App.svelte` reprendre l'intégration fournit dans le dossier integration et transformer cette page en une page svelte qui contiendra 2 scores et 4 boutons pour incrémenter et décrémenter le score finale.

## Énoncé Step-by-step

### 1 - Installation et configuration de SASS

Se positionner à la racine du projet dans le terminal et lancer la commande suivante :
```sh
npm add -D sass
```

Renommer `app.css` en `app.scss` et modifier la ligne d'import dans `main.js`

Terminer en lançant `npm run dev`

### 2 - Intégration
Dans le dosser `./integration` vous trouverez 2 fichiers et un dossier. 

#### 2.1 Styles 
Reprendre le contendu de `./integration/style.scss` et mettre son contenu dans `./src/app.scss`. 

Il faudra également rajouter l'import de la police *Freckle Face* depuis Google Fonts à l'aide de la directive `import` : 
```css 
@import url('https://fonts.googleapis.com/css?family=Freckle Face');
```
L'import doit obligatoirement se trouver à la première ligne du document sinon le précompilateur `vite` vous donnera une erreur.

<details>
<summary>Resultat de app.scss</summary>

```css
/* Les imports doivent rester en première ligne sinon svelte n'aime pas donc avant toute autre directive */
@import url('https://fonts.googleapis.com/css?family=Freckle Face');

html, body {
  height: 100%;
  padding: 0;
  margin: 0;

  #app {
    height: 100%;
    background: #11172a;
  }
}

h1, h2, h3, h4, .font-freckle {
  font-family: 'Freckle Face', sans-serif;
}

...
```
</details>

#### 2.2 HTML

Puis, nous allons déplacer le code contenu entre les balises (inclus) ```<main></main>``` et venir le mettre entre les balises `<script></script>` et `<style></style>` dans notre fichier `./src/App.svelte`

<details>
<summary>Résultat de App.svelte</summary>

```html
<script>
</script>

<main>
  <img src="./images/logo.png" alt="Hot Dog Quiz Logo"/>
  <div class="content">
    <section class="ketchup">
      <h2>KETChUP</h2>
      <div class="content-result font-freckle" aria-label="compteur ketchup 0">
        0
      </div>
      <div class="content-controls">
        <button class="font-freckle" aria-label="boutton décrémentation ketchup">-</button>
        <button class="font-freckle" aria-label="boutton incrémentation ketchup">+</button>
      </div>
    </section>
    <section class="moutarde">
      <h2>Moutarde</h2>
      <div class="content-result font-freckle" aria-label="compteur moutarde 0">
        0
      </div>
      <div class="content-controls">
        <button class="font-freckle" aria-label="boutton décrémentation moutarde">-</button>
        <button class="font-freckle" aria-label="boutton incrémentation moutarde">+</button>
      </div>
    </section>
  </div>
</main>

<style>
</style>

```
</details>


A cet stade, vous allez pouvoir tester à nouveau avec la commande `npm run dev`

<details>
<summary>Rendu attendu</summary>

![screenshot_01](https://user-images.githubusercontent.com/87300647/184116054-71fffc0c-5e66-46c4-96b4-bdeeb509d80a.png)
  
</details>

### 3 - Svelte - Dynamisation
Comme vous pouvez le voir, notre `./src/App.svelte` se décompose en 3 parties : script, html et style.

Dans la partie `<script>` nous allons déclarer deux variables et quatre fonctions :
- Un compteur de points pour chaque équipe que nous allons incrémenter
- Une fonction d'incrémentation et une fonction de décrémentation pour chaque équipe

#### 3.1 Variables 
Pour déclarer une variable, c'est comme en javascript traditionnel : 
```js
<script>
  let ketchup = 0;
  let mustard = 0;
</script>
```
*<small>(N.B. Nous partons sur du let plutôt qu'un const car nous allons venir modifier ces variables par la suite... et une const est de part son nom ... constante !)</small>*

#### 3.2 Fonctions
Ici encore, pour déclarer une fonction dans svelte, c'est comme en javascript traditionnel.

Toujours dans le fichier `./src/App.svelte` et dans la balise `<script>` on ajoute nos quatres fonctions:

```js
  // incrémente le compteur ketchup
  const incrementKetchup = () => {
    ketchup += 1;
  }

  // décrémente le compteur ketchup
  const decrementKetchup = () => {
    ketchup -= 1;
  }

  // incrémente le compteur moutarde
  const incrementMustard = () => {
    mustard += 1;
  }

  // incrémente le compteur moutarde
  const decrementMustard = () => {
    mustard -= 1;
  }
```

#### 3.3 Dynamisation du html
Ici, l'objectif est de venir remplacer les elements statiques par des éléments dynamique, par exemple, dans le html, le 0 statique de l'équipe ketchup : 
```html
  <div class="font-freckle">
    0
  </div>
```
devient :
```html
  <div class="font-freckle">
    {ketchup}
  </div>
```

<small>**N.B. Avec les Svelte, nos variables javascript sont directement écrit dans le code à l'aide d'accolades**</small>

Puis faire la même chose pour le compteur moutarde.

Nous avons quatre boutons, dans la partie HTML, ici pas de `addEventListener` ou `getElementById`, nous allons directement indiquer que lorsqu'on clique sur un bouton, il appelle directement la fonction sous la forme suivante : 
```html 
 <button on:click={decrementKetchup} class="font-freckle">-</button>
```

Répétez l'opération pour les trois autres boutons en prenant le soin de changer la fonction associé à chaque bouton.

<details>
<summary>Resultat attendu pour App.svelte</summary>

```html
<script>
  let ketchup = 0;
  let mustard = 0;

  // incrémente le compteur ketchup
  const incrementKetchup = () => {
    ketchup += 1;
  }

  // décrémente le compteur ketchup
  const decrementKetchup = () => {
    ketchup -= 1;
  }

  // incrémente le compteur moutarde
  const incrementMustard = () => {
    mustard += 1;
  }

  // incrémente le compteur moutarde
  const decrementMustard = () => {
    mustard -= 1;
  }
</script>

<main>
  <img src="./images/logo.png" alt="Hot Dog Quiz Logo"/>
  <div class="content">
    <section class="ketchup">
      <h2>KETChUP</h2>
      <div class="content-result font-freckle" aria-label="compteur ketchup {ketchup}">
        {ketchup}
      </div>
      <div class="content-controls">
        <button on:click={decrementKetchup} aria-label="boutton décrémentation ketchup" class="font-freckle">-</button>
        <button on:click={incrementKetchup} aria-label="boutton incrémentation ketchup" class="font-freckle">+</button>
      </div>
    </section>
    <section class="moutarde">
      <h2>Moutarde</h2>
      <div class="content-result font-freckle" aria-label="compteur moutarde {mustard}">
        {mustard}
      </div>
      <div class="content-controls">
        <button on:click={decrementMustard} aria-label="boutton décrémentation moutarde" class="font-freckle">-</button>
        <button on:click={incrementMustard} aria-label="boutton incrémentation moutarde" class="font-freckle">+</button>
      </div>
    </section>
  </div>
</main>

<style>
</style>


Pensez à tester votre resultat à l'aide de la commande `npm run dev` !

### Bonus

#### B.1 - Pas de points négatifs
Modifiez nos fonctions pour que les points du jeu ne puisse pas être négatif

#### B.2 - DRY
Le code ici n'est pas très DRY (**D**on't **R**epeat **Y**ourself), refactorisez nos quatres fonctions pour ne plus avoir qu'une seule 

<details>
<summary>Indice</summary>

Il est possible d'appeler une fonction anonyme lors d'un événement de type `on:click`. Example : 
```js
<button on:click={() => maFonction('qqzIci')}></button>
```
</details>

#### B.3 - Components
Afin d'éviter de tout avoir dans la même page, il est recommandé de découper son projet en composants réutilisables et c'est même l'un des principes fondamentaux de tous les frameworks web (Svelte, Vue, React etc.)

Les deux blocs de compteurs sont sensiblement identiques, à l'aide de la doc de Svelte [https://svelte.dev/tutorial/nested-components](https://svelte.dev/tutorial/nested-components), découpez nos deux compteurs en deux composants
