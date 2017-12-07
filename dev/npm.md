# Misc. node shit

- [Misc. node shit](#misc-node-shit)
- [Update your dependencies](#update-your-dependencies)
- [Is Browser-sync refreshing slowly?](#is-browser-sync-refreshing-slowly)
- [No Browser-sync in your Gulp?](#no-browser-sync-in-your-gulp)

----

## Update your dependencies

Install npm chekc updates:
```
npm install npm-check-updates -g
```

In your package.json folder:

```
npm-check-updates
npm-check-updates -u
```

You might need to delete your node_modules or update your npm (`brew update npm`).

----

http://www.alwaystwisted.com/articles/updating-dependencies-in-a-packagejson


## Is Browser-sync refreshing slowly?

Are you using a .local domain? Change it to something else like .dev. MacOS uses .local which may be interfering with it.

----

https://stackoverflow.com/questions/24807786/browsersync-extremely-slow

## No Browser-sync in your Gulp?

Launch it separately:

```
browser-sync start -p 'your.local.domain.or.ip.dev' -f './*.php' './*.css' './views/**/*.twig' './js/**/*.js'
```
