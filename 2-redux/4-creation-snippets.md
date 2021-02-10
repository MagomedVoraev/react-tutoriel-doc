# Custom Snippets VS Code

`Fichiers > Préférences > Extraits de code utilisateurs`

`Nouveau fichier d'extraits globaux`

```
"Create component": {
		"scope": "javascript,typescript",
		"prefix": "comp",
		"body": [
			"import React from 'react'",
			"",
			"const $1 = ({$2}) => (",
			"	$3",
			");",
			"",
			"export default $1",
			"",
		],
		"description": "Create a simple component"
	},
	"Import Component": {
		"scope": "javascript,typescript",
		"prefix": "impcomp",
		"body": [
			"import $1 from 'src/components/$1';",
		],
		"description": "Import top level component"
	},
	"Import PropTypes": {
		"scope": "javascript,typescript",
		"prefix": "impprop",
		"body": [
			"import PropTypes from 'prop-types';",
		],
		"description": "Import of PropTypes"
	},
	"PropTypes": {
		"scope": "javascript,typescript",
		"prefix": "proptypes",
		"body": [
			"$1.propTypes = {",
			"	$2: PropTypes.$3",
			"};",
			"",
			"$1.defaultProps = {",
			"	$4",
			"}",
			""
		],
		"description": "Import of PropTypes"
	}
```