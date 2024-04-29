# Code snippets

Used keywords:
* CONFIGURATION

<hr/>

### `__private__` packages enforced by ESLint

```eslintrc.js
module.exports = {
    ...
    plugins: [ ... 'import'],
    rules: {
        ...
        'import/no-internal-modules': [
            'error',
            {
                forbid: ['**/*/__private__/**'],
            },
        ],
    },
};
```

Keywords: CONFIGURATION