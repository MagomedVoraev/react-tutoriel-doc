# Custom Snippets VS Code

- Fichiers > Préférences > Extraits de code utilisateurs

- Nouveau fichier d'extraits globaux : *component.code-snippets*

All created SNIPPETS : 

- `comp`
- `impcomp`
- `impprop`
- `proptypes`
- `store`
- `reducer`
- `container`
- `action`
- `formcomp`
- `storemiddleware`

```
"Create component": {
		"scope": "javascript,typescript",
		"prefix": "comp",
		"body": [
			"import React from 'react';",
			"import PropTypes from 'prop-types';",
			"",
			"import './style.scss';",
			"",
			"const $1 = () => (",
			"	<div className=\"\">Component : $1</div>",
			");",
			"",
			"export default $1;",
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
	},
	"Basic store": {
		"scope": "javascript",
		"prefix": "store",
		"body": [
			"/* eslint-disable no-underscore-dangle */",
			"import { createStore } from 'redux';",
			"",
			"import reducer from './reducer';",
			"",
			"const store = createStore(",
			"  reducer,",
			"  window.__REDUX_DEVTOOLS_EXTENSION__ && window.__REDUX_DEVTOOLS_EXTENSION__(),",
			");",
			"",
			"export default store;",
			""
		],
		"description": "Basic store"
	},
	"Reducer": {
		"scope": "javascript",
		"prefix": "reducer",
		"body": [
			"const INITIAL_STATE = {",
			"  $1",
			"};",
			"",
			"const reducer = (state = INITIAL_STATE, action = {}) => {",
			"  switch (action.type) {",
			"    default:",
			"      return state;",
			"  }",
			"};",
			"",
			"export default reducer;",
			""
		]
	},
	"Container": {
		"scope": "javascript",
		"prefix": "container",
		"body": [
			"import { connect } from 'react-redux';",
			"import $1 from 'src/components/$1';",
			"",
			"const mapStateToProps = (state) => ({",
			"  $2",
			"});",
			"",
			"const mapDispatchToProps = () => ({",
			"  $3",
			"});",
			"",
			"export default connect(mapStateToProps, mapDispatchToProps)($1);",
			""
		]
	},
	"Action": {
		"scope": "javascript",
		"prefix": "action",
		"body": [
			"export const $1 = '$1';",
			"",
			"export const $2 = ($3) => ({",
			"  type: $1,",
			"  $3",
			"});",
			""
		]
	},
	"Form Component": {
		"scope": "javascript",
		"prefix": "formcomp",
		"body": [
			"import React from 'react';",
			"import PropTypes from 'prop-types';",
			"",
			"import './style.scss';",
			"",
			"const $1 = ({ inputValue, setMessageValue, sendNewMessage }) => {",
			"	const handleOnSubmitForm = (event) => {",
			"		event.preventDefault();",
			"		sendNewMessage();",
			"	};",
			"",
			"	const handleOnInputChange = (event) => {",
			"		setMessageValue(event.target.value);",
			"		console.log(event.target.value);",
			"	};",
			"",
			"	return (",
			"		<form className=\"form\" onSubmit={handleOnSubmitForm}>",
			"  			<input",
			"    	  	type=\"text\"",
			"    	  	className=\"form__input\"",
			"    	  	value={inputValue}",
			"    	  	onChange={handleOnInputChange}",
			"    	  	placeholder=\"Saisissez votre message\"",
			"    	  	// ref={inputRef}",
			"  			/>",
			"  			<button type=\"submit\" className=\"form__submit\">Envoyer</button>",
			"		</form>",
			"	);"
			"};",
			"",
			"$1.propTypes = {",
			"	inputValue: PropTypes.string,",
			"	setMessageValue: PropTypes.func,",
			"	sendNewMessage: PropTypes.func,",
			"  };",
			"",
			"$1.defaultProps = {",
			"	inputValue: '',",
			"	setMessageValue: () => {},",
			"	sendNewMessage: () => {},",
			"};",
			"",
			"export default $1;",
		]
	},
	"Store with Middleware": {
		"scope": "javascript",
		"prefix": "storemiddleware",
		"body": [
			"import { createStore, applyMiddleware, compose } from 'redux';",
			"import $1Middleware from 'src/middleware/$1';",
			"import reducer from './reducer';",
			"",
			"const composeEnhancers = window.__REDUX_DEVTOOLS_EXTENSION_COMPOSE__ || compose;",
			"",
			"// On créé le store en lui donnant le reducer afin transformer les actions",
			"// en changement d'état, et pour calculer aussi l'état initial",
			"const store = createStore(",
			"  reducer, /* preloadedState, */",
			"  composeEnhancers(",
			"    applyMiddleware(",
			"      $1Middleware,",
			"    ),",
			"  ),",
			");",
			"",
			"export default store;",
		]
	}
```