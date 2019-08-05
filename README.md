# Laravel Pagination with VueJS (customizable)
[![](https://img.shields.io/npm/dt/vue-laravel-paginex.svg)](https://www.npmjs.com/package/vue-laravel-paginex)
[![](https://img.shields.io/npm/v/vue-laravel-paginex.svg)](https://www.npmjs.com/package/vue-laravel-paginex)

`vue-laravel-paginex` will provide you ability to easily
create pagination from Laravel Pagination object.

## Installation

`npm i vue-laravel-paginex`

or

`yarn add vue-laravel-paginex`

## Usage

First import the Pagination component inside 
your Vue component.
```vue
import Pagination from 'vue-laravel-paginex'
```
and define it 
```vue
Vue.component('Pagination', Pagination)
```

Then you'll be able to use pagination component.

#### Example:

```html
<Pagination :changePage="getData" :data="data"/>
```
`:changePage` prop will run the function 
( in our case is `getData()`) when new page selected.
##### getData() function example with vue-resource.
```javascript
methods: {
    getData(data) {
        this.$http.get('getDataEndpoint?page=' + data.page).then(response => {
            this.data = response.data
        })
    }
}
```
`this.data` object must be Laravel default or API Resource Pagination object.
##### Example:
```javascript
{
    current_page: 1
    data: [{id: 25600, brand_id: 14, number: "47609-253286", name: "Mall of Africa", type: "Licensed",…},…]
    first_page_url: "http://example.com/getDataEndpoint?page=1"
    from: 1
    last_page: 10
    last_page_url: "http://example.com/getDataEndpoint?page=10"
    next_page_url: "http://example.com/getDataEndpoint?page=2"
    path: "http://example.com/getDataEndpoint"
    per_page: 20
    prev_page_url: null
    to: 20
    total: 200
}
```
or
```javascript
{
    "data": [
        {
            "id": 1,
            "name": "Eladio Schroeder Sr.",
            "email": "therese28@example.com",
        },
        {
            "id": 2,
            "name": "Liliana Mayert",
            "email": "evandervort@example.com",
        }
    ],
    "links":{
        "first": "http://example.com/pagination?page=1",
        "last": "http://example.com/pagination?page=1",
        "prev": null,
        "next": null
    },
    "meta":{
        "current_page": 1,
        "from": 1,
        "last_page": 1,
        "path": "http://example.com/pagination",
        "per_page": 15,
        "to": 10,
        "total": 10
    }
}
```

## Customizations

You can customize your pagination styles by overwriting default values.
Available props for component:

Prop Name           | Default Value
-------------       | -------------
containerClass      | pagination
prevButtonClass     | page-item
prevButtonText      | Prev
nextButtonClass     | page-item
nextButtonText      | Next
numberButtonClass   | page-item
numberClass         | page-link
numbersCountForShow | 2
activeClass         | active

##### Example:
`<Pagination :changePage="getData" :data="data" :containerClass="pagination-container"/>`

You can use `:options` prop by passing options object into it.

##### Example:
You have to define here only props which you want to overwrite.
```javascript
options:{
    containerClass: "pagination-container",
    prevButtonClass: "prev-button-class",
    nextButtonText: "Next Page"
    ...
}
```
`<Pagination :changePage="getData" :data="data" :options="options"/>`

##### Example:
You can set your own request params for request
```javascript
params () {
    return {
       keyword:this.keyword
    }
}
```
`<Pagination :changePage="getData" :data="data" :options="options" :requestParams="params"/>`

## Credits

- [Garik Harutyunyan](https://github.com/GHarutyunyan)
- [Lionix Team](https://github.com/lionix-team)
