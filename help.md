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

const books = document.querySelectorAll('#book-list li .name');

# For the case of querySelectorAll , the return value is a set of nodes and not a collection of html and hence can be traversed directly using forEach and need not convert to arrays , but getElementByTagName/getElementByClassName does not do so and thus , we get the return value as collection of html and need to be convertted to arrays before iterating over it.

Array.from(books).forEach(function(book){

# textContext -> access the text present in the element  and += appends the given string to it
  book.textContent += ' (Book title)';
});

const bookList = document.querySelector('#book-list');

# this is can be used to change the existing html structure -- what this 1st line will do is go to the required place where book-list is the css selector and then in it replace its inner value with the given string . For the 2nd part, it will apppend the required value.
bookList.innerHTML = '<\h2\>Books and more books...<\/h2\>';
bookList.innerHTML += '<\p\>This is how you add HTML content<\/p\>';

## lesson 6 ---->

## NODES IN DOM --> everything present in the DOM is a node -- everything present inside a document  is a node - html tag , head tag , body tag etc.   nodes are of various types --> head , tag , comment , attributes

const banner = document.querySelector('#page-banner');

# node type - returns a number - corresponds to element , attribute etc. 
console.log('#page-banner node type is:', banner.nodeType);
console.log('#page-banner node name is:', banner.nodeName);
# not a property like above 2 but method
console.log('#page-banner has child nodes:', banner.hasChildNodes());

# clone a present node
# passing false in this will only return the single line element else true will return everything present inside the element.
const clonedBanner = banner.cloneNode(true);
console.log(clonedBanner);


# LESSON 7 ------>>>> Traverse dom from child -> parent nodes/elements and vice-versa

const bookList = document.querySelector('#book-list');

# next 2 lines provide the same o/p
console.log('book list parent element:', bookList.parentElement);
console.log('book list parent node:', bookList.parentNode);

console.log('all node children:');
Array.from(bookList.childNodes).forEach(function(node){
  console.log(node);
});

console.log('all element children:');
Array.from(bookList.children).forEach(function(node){
  console.log(node);
});

const titles = bookList.querySelectorAll('.name');

console.log('Book titles:');
Array.from(titles).forEach(function(title){
  console.log(title.textContent);
});


## lesson 8 --> traversing the siblings

const bookList = document.querySelector('#book-list');

console.log('#book-list next sibling:', bookList.nextSibling);
console.log('#book-list next element sibling:', bookList.nextElementSibling); # give the next element sibling(actually useful)
console.log('#book-list previous sibling:', bookList.previousSibling);
console.log('#book-list previous element sibling:', bookList.previousElementSibling);

bookList.previousElementSibling.querySelector('p').innerHTML += '<br />Too cool for everyone else!';


## lesson 9 --> DOM events / remove content  --->> EVENT listeners are those which provide 

const listItems = document.querySelectorAll('#book-list ul li');

Array.from(listItems).forEach(function(item){
  item.addEventListener('click', (e) => {

    const li = e.target.parentElement;
    console.log('child element to remove:', li);
    console.log('parent element to remove child from:', li.parentElement);
    li.parentNode.removeChild(li);

  });
});

// prevent default behaviour

const link = document.querySelector('#page-banner a');

link.addEventListener('click', function(e){
  e.preventDefault();
  console.log('Navigation to', e.target.textContent, 'was prevented');
});