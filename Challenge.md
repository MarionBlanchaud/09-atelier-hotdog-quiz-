# Des composants avec Svelte

## Objectifs

Découvrir l'approche composants d'un projet web.

Afin d'éviter de tout avoir dans la même page, il est recommandé de découper son projet en composants réutilisables et c'est même l'un des principes fondamentaux de tous les frameworks web (Svelte, Vue, React etc.)

Les deux blocs de compteurs sont sensiblement identiques, en terme de code. À l'aide de la doc de Svelte [https://svelte.dev/tutorial/nested-components](https://svelte.dev/tutorial/nested-components), nous allons donc découper nos deux compteurs en un seul composant réutilisable et parametrable. C'est bath non ? (On ressort des expressions des années 70 si on veut, non mais !)


## Pas à pas

### Étape 1

Réaliser le petit tutoriel qui consiste à imbriquer un composant dans un autre : [https://svelte.dev/tutorial/nested-components](https://svelte.dev/tutorial/nested-components). Ce tuto est a réaliser directement dans le navigateur.

<details>
<summary>Soluce</summary>

App.svelte

```html
<script>
	import Nested from './Nested.svelte';
</script>
<p>This is a paragraph.</p>
<Nested/>
<style>
	p {
		color: purple;
		font-family: 'Comic Sans MS', cursive;
		font-size: 2em;
	}
</style>
```
</details>

### Étape 2

Nous allons commencer par démarrer le serveur de développement.

<details>
<summary>Soluce</summary>

```bash
npm run dev
```
</details>

Pour cette seconde étape nous allons créer un nouveau composant `<Counter />`.

Souvent, nous crééons un dossier components pour ranger nos composants, donc, acte, créons un dossier `components`. Dans ce dossier nous allons créer un fichier `Counter.svelte`. Comme nous l'avons vu dans le tutoriel, il est courant de nommer les composants avec une majuscule. 

Dans ce composant nous allons écrire `<p>Composant compteur</p>` et nous allons l'ajouter dans `App.svelte` à la suite des 2 compteurs précédents. À la suite des 2 balises `<section>`. Nous devrions avoir : 

```html
<section>
  ...
</section>
<section>
  ...
</section>
<Counter/>
```

Il faut aussi penser à importer notre composant dans le fichier `App.svelte`.

```html
<script>
  // j'importe mon composant. 
  import Counter from "./components/Counter.svelte";
</script>
```

Visuelement, dans le navigateur, nous devrions avoir `Composant compteur` qui apparait à la suite des compteurs.

Nous avons réussi à créer un composant et à l'afficher ! L'étape suivante sera de faire en sorte qu'il affiche un compteur. Comme ça nous pourrons l'utiliser dans notre page. 

### Étape 3

Codons notre composant !

Il sera composé de 2 parties : 

- la partie HTML qui contiendra tout le HTML nécessaire pour afficher un compteur.
- la partie script, qui contiendra tout le js nécessaire pour un compteur.

Nous pouvons dans un premier temps copier coller telle quelle la partie script, par exemple si nous nous basons sur le compteur Ketchup, il nous faut : 
- Un variable qui servira de compteur et sera modifiée à chaque clic, pendant l'atelier c'était les variables `ketchup` et `mustard`. Ici comme nous allons faire UN composant pour UN compteur, nous n'aurons besoin que d'un compteur.
- Une fonction qui permet d'incrémenter et décrémenter notre compteur.

Pour la partie HTML, on peut aussi reprendre le HTML du compteur ketchup par exemple.

Si votre compteur ne s'appelle plus `ketchup`, pensez à le renommer quand vous affichez sa valeur dans le HTML.

Par exemple, si vous avez déclaré une variable `let counter = 0;`, dans le HTML pensez à remplacer `{ketchup}` par `{counter}`.

<details>
<summary>Un exemple de solution pour notre composant (à consulter après avoir essayé ;))</summary>

Counter.svelte

```html
<script>
    let counter = 0;

    const changeCounter = (amount) => {
      // Je modifie le compteur du montant spécifié
      counter += amount;
  
      // Je vérifie qu'après la modification je ne me retrouve pas avec une valeur négative, si tel est le cas, je le repasse à 0
      if (counter < 0) counter = 0;
    };
    
  </script>
  
  <section>
    <h2>Ketchup</h2>
    <div class="font-freckle">
      {counter}
    </div>
    <div>
      <button
        on:click={() => changeCounter(-1)}
        class="font-freckle"
        >-</button
      >
      <button
        on:click={() => changeCounter(1)}
        class="font-freckle"
        >+</button
      >
    </div>
  </section>
  
  <style>
  </style>
  
```
</details>

À la fin de cette étape, nous devrions avoir 3 compteurs qui apparaissent sur la page, 2 écrits en dur dans le fichier `App.svelte` et le 3e affiché grâce à notre composant.

### Étape 4

Pour l'étape suivante nous allons faire en sorte de n'utiliser que nos composants pour afficher des compteurs. Dans le fichier `App.svelte`, nous allons remplacer : 

```html
<section>
  ...
</section>
<section>
  ...
</section>
<Counter/>
```

par

```html
<Counter/>
<Counter/>
```

Comme ça nous aurons bien 2 compteurs qui seront affichés sur notre page. Victoire \o\ /o/ \o/ /o\.

Ou pas.

C'est bien, on a 2 compteurs, si on teste on voit que leur fonctionnement est bien indépendant mais ils sont identiques ! Or nous souhaitons avoir 2 compteurs différents. Ah !

Nous allons donc rendre nos composants parametrables. Il faudrait pour un compteur pouvoir lui spécifier : 
- un titre
- une couleur de fond.

Let's go !

### Étape 5

Nous allons modifier notre composant pour le rendre parametrable. 

Nous allons commencer par remplacer le titre par une variable. 

Nous allons créer une nouvelle variable dans la partie `<script>` du composant.

```js
let title = "Ketchup";
```

Ensuite nous allons remplacer dans la partie HTML le titre du composant par le contenu de notre variable.

Nous allons remplacer 

```js
<h2>KETChUP</h2>
```

Par

```js
<h2>{title}</h2>
```

Normalement, visuelement rien ne change. Sauf que nous avons (presque) rendu notre composant parametrable.

Si nous modifions le contenu variable `title`, nous modifions le titre qui sera affiché.

Sauf que ce que nous voulons faire, c'est modifier le titre lors de l'utilisation du composant, donc dans le fichier `App.svelte`.

Nous allons donc rajouter le mot clef `export` devant la déclaration de notre variable. C'est la façon de Svelte de déclarer une _props_, un donné qu'il est possible de transmettre au composant.

Donc si vous écrivez 

```js
export let title = "Ketchup";
```

Vous pourrez controler le titre lors de l'utilisation du composant de cette façon : 

Fichier `App.svelte` : 

```html
<Counter title="Ketchup"/>
<Counter title="Moutarde"/>
```

En utilisant l'attribut `title`, nous pouvons controler le contenu de la variable `title` du composant, parce que nous l'avons rendu parametrable grâce au mot clef `export`.

Nous pouvons donc utiliser le composant autant de fois que nous le souhaitons, avec autant de titres différents.


### Étape 6 - Bonus

Rajouter les props que vous imaginez à notre composant `Counter.svelte`. Voire même, créez un composant et essayez de l'utiliser. Faites chauffer votre imagination !
