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
- `reducerIndex`
- `middleware`

```JSON
{
	// Place your global snippets here. Each snippet is defined under a snippet name and has a scope, prefix, body and 
	// description. Add comma separated ids of the languages where the snippet is applicable in the scope field. If scope 
	// is left empty or omitted, the snippet gets applied to all languages. The prefix is what is 
	// used to trigger the snippet and the body will be expanded and inserted. Possible variables are: 
	// $1, $2 for tab stops, $0 for the final cursor position, and ${1:label}, ${2:another} for placeholders. 
	// Placeholders with the same ids are connected.
	// Example:
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
		"prefix": "storeNoMiddleware",
		"body": [
			"/* eslint-disable no-underscore-dangle */",
			"import { createStore } from 'redux';",
			"",
			"import reducer from 'src/reducer';",
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
			"// créer plusieurs fichiers dans le dossier reducers",
			"const INITIAL_STATE = {",
			"  $1",
			"};",
			"",
			"export default (state = INITIAL_STATE, action = {}) => {",
			"  switch (action.type) {",
			"    default:",
			"      return state;",
			"  }",
			"};",
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
			"import $1Middleware from 'src/middlewares/$1';",
			"// on importe le dossier reducers",
			"import rootReducer from 'src/reducers';",
			"",
			"const composeEnhancers = window.__REDUX_DEVTOOLS_EXTENSION_COMPOSE__ || compose;",
			"",
			"// On créé le store en lui donnant le reducer afin transformer les actions",
			"// en changement d'état, et pour calculer aussi l'état initial",
			"",
			"const enhancers = composeEnhancers(",
			"  applyMiddleware(",
			"	 // ici, nous rajoutons tous les middlewares + IMPORT",
			"    $1Middleware,",
			"  ),",
			");",
			"",
			"const store = createStore(rootReducer, enhancers);",
			"",
			"export default store;",
		]
	},
	"Index Reducer combineReducers": {
		"scope": "javascript",
		"prefix": "reducerIndex",
		"body": [
			"// ce fichier sera crée dans le dossier reducers et sera nommé index.js",
			"import { combineReducers } from 'redux';",
			"import $1 from './$1';",
			"import $2 from './$2';",
			"",
			"export default combineReducers({",
			"  $1,",
			"  $2,",
			"});",
		]
	},
	"Middleware React : store, next, action": {
		"scope": "javascript",
		"prefix": "middleware",
		"body": [
			"// nous sommes dans src/middlewares/nomDuFichier.js",
			"// j'importe ACTION et son fichier",
			"import { $1 } from 'src/actions/$2';",
			"",
			"export default (store) => (next) => (action) => {",
			"  console.log('je suis dans le middleware');",
			"  switch (action.type) {",
			"    case $1:",
			"    // ...",
			"    break;",
			"  }",
			"};",
		]
	}
}

```