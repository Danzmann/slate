---
title: API Reference

language_tabs: # must be one of https://git.io/vQNgJ
  - javascript

toc_footers:
  - <a href='#'>Sign Up for a Developer Key</a>
  - <a href='https://github.com/lord/slate'>Documentation Powered by Slate</a>

includes:
  - errors

search: true
---

# Introduction

FieldForce Front-End React Documentation

This example API documentation page was created with [Slate](https://github.com/lord/slate). Feel free to edit it and use it as a base for your own API's documentation.

# File Structure

> Root source files

```
.
|-- index.js
|-- App.js
|-- Main.js
|-- routes.js
|-- create-router.js
|-- components
    |-- <Container Folders for Apps Component>
|-- componentMain
    |-- <Container for Main Component>

```

The index is located in project main folder as `react_index.html`

The source folder is located in `/static/ffreact`

The file structure follows the logic of [Ducks File system](https://medium.com/building-crowdriff/react-redux-file-architecture-ducks-it-up-6b32eaaba341).
Main React App files are located in React root `/static/ffreact`. Root contains files necessary for start function of React app (`index.js`, `App.js`, etc).

From root App branches to componentMain and components.

## Ducks Structure

Each component is wrapper in a folder under `root/components` and each component wrap consists of a Redux folder and a Container folder for defining the functionalities
in the App and also a Translations folder containing the json translation files, read more on [Translation System](#translation-system).

## Component Container

> Example of ProductsApp file structure

```
|-- components
    |-- ProductsApp
        |-- Container
            |-- views
                +-- productListingView.pug
                +-- productsHeaderView.pug
                +-- productGroupsView.pug
            |-- style
                +-- products.styl
                +-- productGroups.styl
            +-- ProductsApp.js
            +-- ProductsMain.js
            +-- ProductGroupsMain.js
            |-- Product
                |-- productDetailViews
                    +-- detail_info.pug
                    +-- detail_sales.pug
                    +-- <other views>
                |-- productDetailStyle
                    +-- detail_info.styl
                    +-- <other styles>
                +-- ProductDetail.js
                +-- ProductCompanyLinkModal.js
                |-- ProductDetailGroups
                    |-- productDetailGroupsViews
                    |-- productDetailGroupsStyle
                    +-- ProductDetailGroups.js
                    +-- productAddGroupsModal.js
                |-- ProductDetailStructure
                    |-- <...>
                |-- <Other Sub Component Containers>
            |-- ProductGroup 
                |-- <...>
        |-- Redux
    |-- <Other Apps Components>
```

> Generic App File structure

```
|-- components
    |-- SomeApp
        |-- SomeComponentContainer
            |-- views
            |-- style
            +-- ComponentController.js
            |-- SubComponent
                |-- subComponentViews
                |-- subComponentStyle
                +-- SubComponentController.js
                |-- <...>
        |-- SomeComponentRedux
```

The Container folder contains all that is responsible for the React component that constitutes the respective App, that is, the main "App" Component, it's pug view files and stylus style, any further assets and also each router view Component.

As in ProductsApp in the provided example, the "App" React component controller is the main view endpoint which is called directly from [Main.js]() and each other component
present in the Container is modeled after a router view. That is, the `ProductsApp.js` is merely a wrapper for two different routing views switchable by, in the case of productsApp, Tabs:

Products and ProductsGroup views, each view has it's own containers, `Product` and `ProductGroup`.

Each of these two views Containers contains it's own React Controller JavaScript file, it's own views and style and also further routing nested in it, and as such, 
they contain further nested Components for each route view. In the example of `Product` component, further views redirect to `ProductDetail`, `ProductDetailGroups`, `ProductDetailStructure`, and so on,
each with it's own React component controller, view, style and further assets if required and the pattern repeats.

Wrapping up the example, for reaching the Products Validity, there are three full components `ProductsApp.js` -> `ProductDetail.js` -> `ProductDetailValidity.js`
due to three routing views MainMenu to Products List, Products List to Single Product Detail, Single Product Detail to Validity.

Based on this example it's not possible to build a generic component structure.

## Redux Container

```
|-- components
    |-- SomeApp
        |-- Container
        |-- Redux
            +-- someAppReducer.js
            +-- someAppActions.js
            +-- someAppConstants.js
        +-- index.js
```

The second folder present in the standard App wrap is the Redux folder which contains all necessary Redux files and services for all API used in the app.
That is, reducers, actions and constants, read more about the [Redux Structure]().

The index file provides access to the redux actions and services to the component and other components.

## Translation System

```

```

The third folder inside the App structure contains the translations files regarded to this App, each Translation file is a json with keys serving as ids for 
linking to the component view and values are arrays of possible translations, organized, currently, as follows:

`[English, Finnish, Russian]`

The order and further languages can be set up and reorganized in the Translation Component set up in the initializer in [App.js]() and language choice can be set in
the `setLanguages()` in [Navbar.js]()


## ComponentMain

ComponentMain folder wrapps the React Component and Redux for the main component, which controls the view, routing, navbar, menu and other essential functionalities.

```
|-- componentMain
    |-- Main
        |-- Navbar.js
        |-- Menu.js
    |-- Redux
        |-- mainReducer.js
        |-- mainActions.js
        |-- mainConstants.js
        
        |-- salesmanReducer.js
        |-- salesmanActions.js
        |-- salesmanConstants.js
```

Kittn uses API keys to allow access to the API. You can register a new Kittn API key at our [developer portal](http://example.com/developers).

Kittn expects for the API key to be included in all API requests to the server in a header that looks like the following:

`Authorization: meowmeowmeow`

# Redux

## Redux structure

> Example of constants use

> Defining a constant

```javascript
export const PRODUCT_SUCCESS = "PRODUCT_SUCCESS";
```

> Using the constant in action and reducer

```javascript
import {PRODUCT_SUCCESS} from "./productsContants";

// Action dispatch object
export const productSuccess = () => ({
    type: PRODUCT_SUCCESS,
});

// Reducer
switch (action) {
  case PRODUCT_SUCCESS:
      return {
          ...state,
          // Reducer stuff goes here
      };
}
```

Due to the Ducks File system used by the project, as described [here](#file-structure), each component has it's own Redux container,
containing it's reducers, action creators and constants and an index file.

Each Redux container is composed of one or more `reducer`, one or more `actions` and one or more `contants` files.

`Reducer` files contain nothing more then the reducer and initialState, exported always as 
`export const reducer = (state = initialState, action)`, the reducer is renamed and specified when being imported by the [index](#index-and-services) file.

`Actions` files contain nothing more then the actions and dispatch objects required

`Contants` files contain nothing more then exported constants containing a string that symbolizes an action, this is used for
avoiding mispeling errors in case of dozens of different actions and makes debugging easier. 

## Component controlled Redux State

### Reducer structure

> Example of component controlled products state

```javascript
const initialState = {
    active_product: {
        comserno: "",
        prodname: "",
        prodsern: "",
        // Other parameters
    },
    // Main list of all products to be displayed in table
    product_list: [],
    page: 0,
    has_more: true,
    error: null,
    prod_simple_response: {
        method: "",
        response: "",
        data: ""
    }
}
```

Each component's redux follows a standard pattern for dealing with the common "list of objects" with "active object" present in the App's,
such as Surveys, Products, Accounts, etc, each App contains a base of list of items to be shown and an active object that is selected
from that list. As such, the component Redux is the obvious best option for keeping the list of objects and active object accessible through all of
the different components (as described in [Component Container](#component-container)).

Each App may contain one or more redux bundles (reducer + actions + constants), such as Products App (Redux bundle for products and another for
product groups), and the standard controlled state is replicated for as many different reducers, logically.  

The standard pattern of dealing with App global redux state's begins with the state. The state is comprised of 5 basic entries: 
`items_list`, `active_item`, `item_response` and `error`:

`item_list` is an array that contains the list of item objects to be shown, such as the list of products in the productsApp example.

`active_item` is the currently active item selected from that list, to be shown/modified/deleted/etc.

`item_response` is the object that stores the response for that reducer, more on [Component Redux Responses]()

`error` contains the error message to show to user (or not) more on [Component Error system]()

Components that use pagination system have 2 more required states:

`has_more` determines if the list is fully retrived or more pages are available

`page` keeps track of current page index

### Actions structure

> Example of action creators and dispatch objects

```javascript
// Action  creator
export const action = (data) => {
    // Does something with data
    dispatch(actionDispatchObject(data));
};

// Dispatch object function
const actionDispatchObject = (data) => ({
    type: ACTION_CONSTANT,
    payload: data
});
```

Actions are composed of an action creator and dispatch object. Action creators are called from [index.js](#index-and-services), receive data, perform some operations with this data and dispatch one or more auxiliary actions,
which are the dispatch objects previously described, accordingly.
 
In case of an action which is a simple object with type and other optional parameters, that is, an action that does not contain any logic but a simple dispatch object. The
dispatch object itself may be exported as the action creator.

## Managing controlled state

### Asynchronous Actions

> Example of async action with simplified version of GET product

```javascript
export const getProduct = (baseURL, prodsern) => {

    return dispatch => {

        dispatch(mainActions.setLoadingInfo(true));

        axios.get(baseURL + '/api/products/' + prodsern + '/', {})
            .then(response => {
                let data = response.data.data;

                dispatch(mainActions.setLoadingInfo(false));
                dispatch(productSelect(data));
            })
            .catch(error => {
                dispatch(mainActions.setLoadingInfo(false));
                dispatch(productFailure(error.message, "show"));
            });
    }
};
```

> Continuing the example above, the two dispatch objects used by the successfull and failed responses

```javascript
export const productSuccess = (action, data=null) => ({
    type: PRODUCT_SUCCESS,
    action: action,
    payload: data,
});

export const productFailure = (error, method) => ({
    type: PRODUCT_FAILURE,
    payload: error,
    action: method
});
```

Most of the App's Component Redux state is modified by the means of async HTTP operations, so here the Redux actions server as HTTP service
for the component, performing all requests and storing the necessary information in the state.
Due to the async nature of the operations, the use of [Redux Thunk Middleware]() is required.

The actions are organized as one action for performing the async operation using axios, this action solely performs the request and other actions, or [dispatch objects]() will
dispatch the object containing the data to the reducer.

Once the action has been called, the main Reducer's `setLoadingInfo()` action will be called (more information on main reducers actions [here](#main-redux)),
then after performing the request, the promise will be dealt with by axios and besides resetting the main reducer's `loadingInfo`, a [dispatch object]() will be dispatched
according to whether the promise resolved or failed, with appropriate data.

<aside class="warning">
Due to the back-end API standard return format, the request data is get as "response.data.data", as the regular "response.data" from
axios contains the whole API response, with "data" and "links"
</aside>

### Standard Actions for controlled state

YADADDAYADADAAYADDDAYADDAYADDAYADDAYADDAYAADA

## Index and Services

> Index exporting generalized accountActions variable that contains all actions 

```javascript
import * as _accountActions from "./Redux/accountActions";
export {_accountActions as accountActions};

```

> Index file service example

```javascript
export function productService(action, baseURL=false, params={}) {

    if (action === "show" || action === "delete" || action === "put") {

        if (!("prodsern" in params)) {
            return mainActions.devErrorHandler("Product serial number is not defined");
        }
    }

    switch(action) {

        // gets information of single product
        case "show":
            return _productActions.getProduct(baseURL, params.prodsern, params.index);

        // gets list of all products
        case "index":
            if (!('p' in params)) {
                return mainActions.devErrorHandler("Page is not defined");
            }
            return _productActions.getProductsPage(baseURL, params);

        // performs delete request for specific product
        case "delete":
            return _productActions.deleteProduct(baseURL, params.prodsern, params.withCompounds);

        // performs update put request for specific product
        case "put":
            return _productActions.updateProduct(baseURL, params.product, params.prodsern);

        // performs creation of new product on post request 
        case "post":
            return _productActions.createProduct(baseURL, params.product);

        // changes data on active product
        case "input":
            return _productActions.inputActiveProduct(params.key, params.input);

        // MORE CASES....
    }
}
```

Each App Component usually has it's own `index.js` file in root of the App Wrapper, the index file imports all
actions and constants from Redux container and exports as a unified variable in which all actions can be accessed as a method.

The actions can be imported by any component for the dispatch to be [mapped to props](), but to avoid having dozens of actions mapped into a component's
props, the index exports the `componentService` that follows the prototype `componentService(action, baseURL=false, params={});`

The service will map all actions from a certain component and provide a single wrapper function that can performs multiple action by switching a 
action provided when calling the service from the component props by simply indicating the action as the first parameter.

Optional `baseUrl` parameter must be provided for async actions that perform an HTTP request and `params` optional parameter provides
any kind of additional data that is required by the action in the form of a dictionary object, the specific parameters for the action are extracted from the
`params` parameter.  

All services possess general actions such as `show`, `index`, `delete`, and any other specific action for the component as well as mandatory actions for
components dealing with listing of multiple and active items (such as products, accounts, surveys, etc), such as `input`, `reset`, `reset_list`, read more on
[Component Controller Redux](), as well as the mandatory `reset_response` action, read more on [Component Redux Responses]()


# Style and Structure Standards

## Ff standards

The WebApp possesses a series of standard classes and stylus/pug functions that are used throughout all Apps to keep the same style norms.
There are (currently)  7 basic generic styling norms, as follows:
operations:

`ff-table` For the creation of tables

`ff-forms` For the creation of all kinds of input forms

`ff-content` For the creation of main content pages

`ff-modal` For the creation of modal windows

`ff-tabs` For the creation of header tabs

`ff-datepicker` For the creation and use of datepicker

`ff-buttons` For the creation of bootstrap-like buttons

`utilites` Contains many different small style operations 

# Kittens

## Get All Kittens

```ruby
require 'kittn'

api = Kittn::APIClient.authorize!('meowmeowmeow')
api.kittens.get
```

```python
import kittn

api = kittn.authorize('meowmeowmeow')
api.kittens.get()
```

```shell
curl "http://example.com/api/kittens"
  -H "Authorization: meowmeowmeow"
```

```javascript
const kittn = require('kittn');

let api = kittn.authorize('meowmeowmeow');
let kittens = api.kittens.get();
```

> The above command returns JSON structured like this:

```json
[
  {
    "id": 1,
    "name": "Fluffums",
    "breed": "calico",
    "fluffiness": 6,
    "cuteness": 7
  },
  {
    "id": 2,
    "name": "Max",
    "breed": "unknown",
    "fluffiness": 5,
    "cuteness": 10
  }
]
```

This endpoint retrieves all kittens.

### HTTP Request

`GET http://example.com/api/kittens`

### Query Parameters

<aside class="notice">
You must replace <code>meowmeowmeow</code> with your personal API key.
</aside>


Parameter | Default | Description
--------- | ------- | -----------
include_cats | false | If set to true, the result will also include cats.
available | true | If set to false, the result will include kittens that have already been adopted.

<aside class="success">
Remember — a happy kitten is an authenticated kitten!
</aside>

## Get a Specific Kitten

```ruby
require 'kittn'

api = Kittn::APIClient.authorize!('meowmeowmeow')
api.kittens.get(2)
```

```python
import kittn

api = kittn.authorize('meowmeowmeow')
api.kittens.get(2)
```

```shell
curl "http://example.com/api/kittens/2"
  -H "Authorization: meowmeowmeow"
```

```javascript
const kittn = require('kittn');

let api = kittn.authorize('meowmeowmeow');
let max = api.kittens.get(2);
```

> The above command returns JSON structured like this:

```json
{
  "id": 2,
  "name": "Max",
  "breed": "unknown",
  "fluffiness": 5,
  "cuteness": 10
}
```

This endpoint retrieves a specific kitten.

<aside class="warning">Inside HTML code blocks like this one, you can't use Markdown, so use <code>&lt;code&gt;</code> blocks to denote code.</aside>

### HTTP Request

`GET http://example.com/kittens/<ID>`

### URL Parameters

Parameter | Description
--------- | -----------
ID | The ID of the kitten to retrieve

## Delete a Specific Kitten

```ruby
require 'kittn'

api = Kittn::APIClient.authorize!('meowmeowmeow')
api.kittens.delete(2)
```

```python
import kittn

api = kittn.authorize('meowmeowmeow')
api.kittens.delete(2)
```

```shell
curl "http://example.com/api/kittens/2"
  -X DELETE
  -H "Authorization: meowmeowmeow"
```

```javascript
const kittn = require('kittn');

let api = kittn.authorize('meowmeowmeow');
let max = api.kittens.delete(2);
```

> The above command returns JSON structured like this:

```json
{
  "id": 2,
  "deleted" : ":("
}
```

This endpoint deletes a specific kitten.

### HTTP Request

`DELETE http://example.com/kittens/<ID>`

### URL Parameters

Parameter | Description
--------- | -----------
ID | The ID of the kitten to delete

