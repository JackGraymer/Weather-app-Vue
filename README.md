# weather app

This project is a simple weather app using Vue 3 in Vite.

The motivation is to start learning Vue and it's perks to able in the future, to make better choices when choosing a framework.

### How it works

Pretty simple, the search bar value is used for the fetch of the weather API. If the city exists and the fetch is succesful, then the wrapper will be visible as it depends on the response data not being `undefined`.

After the data is retrieved, it is shown, changing the image depending on the temperature.

## Project Setup
>This commands can be found in `package.json` in the `script` tag.

```sh
npm install
```

### Compile and Hot-Reload for Development

```sh
npm run dev
```

### Compile and Minify for Production

```sh
npm run build
```
### Preview the production version

```sh
npm run preview
```