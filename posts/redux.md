---
title: 'redux and its components'
date: '2021-02-02'
---
**redux**

For state maintenance

*State :*

When any operation or an event happened in a web page, the state of that page will be stored. state is simply a javascript object.

Example: when a button is clicked to open a form, then the button clicked will be true, an empty object will be opened for the newly opened form and every change made to the app will result in updating the state object. this is called the state or the state tree.

We can not edit state, we can only modify a state by action.

---

To describe state mutations, we have to write a function that takes the previous state of the app,  action being dispatched and returns a next state of the app, this function must be a pure function. this function is called the reducer.

function **reducer** (state, action) {

return nextState;

}

---

**createStore** a redux component that returns an object of methods like getState, dispatch, subscribe.

import {createStore} from 'redux'

getState - will display the state of the app,

dispatch- will operate on the action of the app,

subscribe- will render the changes to the app.

---

**connect**  a react-redux component used to combine the objects returned from functions and provide them as props along with the props of parent component to any other parent component

example:

import {connect} from 'react-redux'

const Parent1 = connect(function1, function2)(Parent2);

function1 (){

return {data}

}

function2 (){

return {id}

}

below does the same job without connect.

const Parent1 = (props )⇒{

return(

<Parent2  prop1 = {data} prop2 = {id}>

);

}

---

<provider> , context

To avoid dependency in the code, we pass global variables as properties to the components.
To pass properties to child components in a neat way by using provider component.

Instead of passing props by parent component we can bind parent component with provider and pass props to provider component.
before :

ReactDOM.render(<App store = {createStore(reducer)}/>, document.getElementById('root'));

After:

ReactDOM.render(<Provider store = {createStore(reducer)}>
<App/>
</Provider>, document.getElementById('root'));

provider component can be imported from react-redux

import {Provider} from 'react-redux';

**What exactly will Provider do** :

const Provider = ()=>{
getChildContext(){
return{
store : props.store
};
}        // this store will be passed as context to children and grand children bind insider provider
return(props.children);
};

**condition for this context to work :**

Provider.childContextTypes = {
store : React.propTypes.object
} ;         // if this is not specified no child will receive store as a context.

we have to specify this for each child components as well to receive the context.

In presentational components we need to get store from context but not props. like {store} = context;
In functional components, we get context as second arguments where as first argument is props. like Footer(props, context){

};
