1. DOM -> Document object model-> change performed on the existing html and css structures or elements , make changes in href , src , alt . create new html elements , attach buttons etc.

2. Get element by id -> Inspect page by source -> go to console -> type document -> this will display all the summarize form of the web page . In order to get element by id ->  we just need to see the unique id associated with it and use -> document.getElementById('unique id') --> unique id of the element which is enclosing our req work

on doing var =  document.getElementById('unique id')  --> pressing enter - will return undefined .. but on typing var -> will print the element  

3. get element by class or tag name --> in headers -> we have class name e.g. h1 class="title"

var t = document.getElementByClassName('title')

t -> print collection of elements of all elememnt with class=title -> this is not a array but a collection .. foreach will not work and hence we need to convert it to a  array to process it.
to use the req one .. use indexing like t[0] , t[1]

get element by tag name --> e.g. <ul> , <li> 
 
var t = document.getElementByTagName('li') -> give an array of li wherever they are used

collections -> array -=>  