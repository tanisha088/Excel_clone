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


## lesson 9 --> DOM events / remove content  --->> EVENT listeners are those which provide us to click and respond to various tasks 

const listItems = document.querySelectorAll('#book-list.delete');

Array.from(listItems).forEach(function(item){

# the click is the event which is present here and (e) defines the callback function which gets fired when we perform the click event by clicking on it . Now, in this case, what we want to do is that when we are clicking on the delete button (since the listitems will be having reference to all the delete buttons , and for each item , when we are attaching a click working with it , on clicking on it , the callback  will activate the function , what we want on delete is to delete the items in li , so we get the e.target{actual delete button}.parentelement -> give the li , and now to delete this li , we will get its parent ui and then delete its child li by li.parentNode.removeChild ... so now, we have added the functionality with the delete button, (item.add) that when it is clicked , the list gets deleted)
  item.addEventListener('click', (e) => {

    const li = e.target.parentElement;
    console.log('child element to remove:', li);
    console.log('parent element to remove child from:', li.parentElement);
    li.parentNode.removeChild(li);

  });
});

// prevent default behaviour

const link = document.querySelector('#page-banner a');

## this has been done to change the default behaviour, what we did was get the href line and add the functionality that whenever clicked --> we prevent the default functioning from happening , i.e. clicking on the link won't take to the given website.
link.addEventListener('click', function(e){
  e.preventDefault();
  console.log('Navigation to', e.target.textContent, 'was prevented');
});


### lesson 10 ---->  EVENT BUBBLING  ---> 

Instead of associating a "delete" button clicking functionality with each of the buttons present separately .. what we can do is that we attach the click functionality with the ul , i.e. the parent of parent of the delete buttons. And when only when the click has been made on the delete button , we will delete the corresponding list , else if anywhere else , we will do nothing. This is a lot easier then what was being done earlier.


const list = document.querySelector('#book-list ul');

// delete books
list.addEventListener('click', (e) => {
  if(e.target.className == 'delete'){
    const li = e.target.parentElement;
    li.parentNode.removeChild(li);
  }
});


### lesson 11 ---->  Interacting with forms 

const forms = document.forms;
console.log(forms);
# This provides us the forms present along with their id's  and passing the id - gives the exact present form 
console.log(forms['add-book']);

Array.from(forms).forEach(function(form){
  console.log(form);
});

# here what we did was :: 1) prevented the default behaviour of the add-book - e -> denoting the addform-> which actually has add-book -> which has default property of refreshing the page when clicked and hence -> we prevent its default behaviour 2) take a input i.e. it should be such that when we add a value to the addform form , the platform accepts it and display it to the screen 
const addForm = forms['add-book'];
addForm.addEventListener('submit', function(e){
  e.preventDefault();

  # Accepts the input given to it -> and stores in the value variable
  const value = addForm.querySelector('input[type="text"]').value;
  console.log(value);
});


### lesson 12 --->  adding info via the form/ button

const list = document.querySelector('#book-list ul');
const forms = document.forms;

// delete books
list.addEventListener('click', (e) => {
  if(e.target.className == 'delete'){
    const li = e.target.parentElement;
    li.parentNode.removeChild(li);
  }
});

// add books
const addForm = forms['add-book'];
addForm.addEventListener('submit', function(e){
  e.preventDefault();

  // create elements
  const value = addForm.querySelector('input[type="text"]').value;

  # we got the required value we got of the book name and similar to how the other books were present , in order to save this book name , we need to create li, span of bookname and span tag for deleteBtn..... and then add the text content value and then append to the DOM using appendChild 
  const li = document.createElement('li');
  const bookName = document.createElement('span');
  const deleteBtn = document.createElement('span');

  // add text content
  bookName.textContent = value;
  deleteBtn.textContent = 'delete';
  # delete will come after bookName

  // append to DOM
  li.appendChild(bookName);
  li.appendChild(deleteBtn);
  # append li to ul as its child 
  list.appendChild(li);
  //list.insertBefore(li, list.querySelector('li:first-child'));

  // add classes
  # If this wasn't added then the book name would be shown as it is , but the delete button wouldn't show up since we haven't added the required class name acc to which it will function , and also we can add class name like bookName.className+= " name"  but this is generally messy so we use classlist.add and remove 
  bookName.classList.add('name');
  deleteBtn.classList.add('delete');
});


#### lesson 13 ------> changing styles and classes --> added classname to the above

#### lesson 14 ------->  ATTRIBUTES 

book.getAttribute('')-> can be class or href etc.
book.setAttribute('element','new value')
book.has/remove/set/getAttribute

##### lesson 15 ----->  checkboxes and change events 

# when box is checked -> hide everything else display all
// hide books
const hideBox = document.querySelector('#hide');
hideBox.addEventListener('change', function(e){
  if(hideBox.checked){
      #ul mei jo hai sabka display none kar dia
    list.style.display = "none";
  } else {
    list.style.display = "initial";
  }
});


### lesson 16 ----->   CUSTOM SEARCH FILTER :::: 

// filter books
const searchBar = forms['search-books'].querySelector('input');
searchBar.addEventListener('keyup', (e) => {
  const term = e.target.value.toLowerCase();
  const books = list.getElementsByTagName('li');
  Array.from(books).forEach((book) => {
    const title = book.firstElementChild.textContent;
# indexOf will give the index of e.target.value (the value given as input) in the title string and if any the input value is anywhere occuring inside the title .. then we will keep it else not  
    if(title.toLowerCase().indexOf(e.target.value) != -1){
      book.style.display = 'block';
    } else {
      book.style.display = 'none';
    }
  });
});


# lesson 17 ----->>> 

// tabbed content
const tabs = document.querySelector('.tabs');
const panels = document.querySelectorAll('.panel');
tabs.addEventListener('click', (e) => {
  if(e.target.tagName == 'LI'){
    const targetPanel = document.querySelector(e.target.dataset.target);
    Array.from(panels).forEach((panel) => {
      if(panel == targetPanel){
        panel.classList.add('active');
      }else{
        panel.classList.remove('active');
      }
    });
  }
});

