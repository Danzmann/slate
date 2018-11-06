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

Due to the Ducks File system used by the project, as described [here](#file-structure), each component has it's own Redux container,
containing it's reducers, action creators and constants and an index file.

## Services

Before digging into the reducer components


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

