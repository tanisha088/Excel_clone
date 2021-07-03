1. DOM -> Document object model-> change performed on the existing html and css structures or elements , make changes in href , src , alt . create new html elements , attach buttons etc.

2. Get element by id -> Inspect page by source -> go to console -> type document -> this will display all the summarize form of the web page . In order to get element by id ->  we just need to see the unique id associated with it and use -> document.getElementById('unique id') --> unique id of the element which is enclosing our req work

on doing var =  document.getElementById('unique id')  --> pressing enter - will return undefined .. but on typing var -> will print the element  

3. get element by class or tag name --> in headers -> we have class name e.g. h1 class="title"

var t = document.getElementByClassName('title')

t -> print collection of elements of all elememnt with class=title -> this is not a array but a collection .. foreach will not work and hence we need to convert it to a  array to process it.
to use the req one .. use indexing like t[0] , t[1]

get element by tag name --> e.g. "ul" , "li" 
 
4. var t = document.getElementByTagName('li') -> give an array of li wherever they are used


## lesson 3  -> iterating over the set of  collection of elements 

collections -> array 

## lesson 4 -> Query selector 

# THIS IS USED TO GET THE REQUIRED ELEMENT USING THE QUERYSELECTOR --> WITH THE HELP OF CSS SELECTOR 
const wmf = document.querySelector('#book-list li:nth-child(2) .name');
console.log(wmf);

# The css selector above was that in the div of book-list , we had a li - and the 2nd li had the class with id = name and hence when we did these, we got the required result 

# The only issue is that this will only return *********1 return value always************
# so if we want multiple results then use querySelectorAll
var books = document.querySelector('#book-list li .name');
console.log(books);

# even for 1 value , we will get the result in form of selector
books = document.querySelectorAll('#book-list li .name');
console.log(books);

Array.from(books).forEach(function(book){
  console.log(book);
});


## lesson 5 ---> 