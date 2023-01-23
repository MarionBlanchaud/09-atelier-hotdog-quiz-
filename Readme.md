# Template de projet SVELTE

Ce repo peut te servir de point de départ pour tous tes projets Vite + Svelte + Sass !

## Comment utiliser ce repo ?

Il suffit de faire un `Use this template` sur Github et rouler jeunesse 😎

Après l'avoir cloner, il n'y a que quelques commandes à lancer avec de coder :

1. Se placer dans le dossier projet avec `cd projet`
2. Installer les dépendances nécessaires avec `npm install`
   1. Elles sont spécifiées dans `package.json` et seront téléchargées dans `node_modules`
3. Lancer le serveur de dev avec `npm run dev`
4. Aller sur l'adresse fournie par le terminal !

## Où coder et quoi coder ?

* `index.html` ; ici on modifie le `head` de la page, pas plus
* `src/main.js` ; à priori on ne fait rien de plus dedans
* `src/App.svelte` ; le composant principal, c'est le coeur de notre site, le chef d'orchestre des sous-composants
* `src/lib/` ; le dossier dans lequel on mettra tous nos petits composants
* `src/app.scss` ; le fichier principal de notre style
* `src/sass/` ; le dossier où mettre tous les partials sass

## Comment j'ai créé ce repo ?

1. Création d'un dossier sur mon PC de dev
2. Initialisation de Svelte + Vite dans le sous-dossier `projet`

`npm create vite@latest projet -- --template svelte`

3. Déplacement du terminal dans `projet` avec la commande `cd projet`
4. Installation de Sass avec la commande `npm add -D sass`
5. Suppression du contenu inutile du template Svelte
   1. Vidage de `src/app.css`
   2. Suppression des fichiers `src/lib/Counter.svelte`, `src/assets/*` et `public/*` 
   3. Remise à zéro du fichier `App.svelte`

```html
<script>

</script>

<main>
  
</main>

<style>

</style>
```

6. Renommage du fichier `src/app.css` en `src/app.scss`
7. Modification de l'import dans le fichier `src/main.js`

`import './app.css'` => `import './app.scss'`
