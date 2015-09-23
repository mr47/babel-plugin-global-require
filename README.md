## `babel-plugin-global-require`

A simple plugin that allows you to require globally. You just
need to define the *root* directory of your project and this plugin will generate a global alias map.

It's convention based: the alias is always the name of the file. For example:
```
src (root)
  deep
    deep
      deep
        sum.js
      NuclearEventEmitter.js
```

With this plugin, you can:
```JS
import NuclearEventEmitter from 'NuclearEventEmitter'
import sum from 'sum'
```

It will translate `'NuclearEventEmitter'` to `src/deep/deep/NuclearEventEmitter.js` for you. And the same happens to `sum`.

### But what about conflicts?
Given the following structure:
```
src
  deep
    math
      sum.js
      div.js
  math
    sum.js
    div.js
```

You can't require `sum.js` or `div.js` only by its name, because it could result in a require of the file you don't want. So, for this specific case, the conflict is resolved simply by going up one directory (and it keeps going until there's no conflict):
```JS
import sum from 'math/sum'
import div from 'deep/math/div'
```
