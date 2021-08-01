1. This is an excel clone with  grid being : columns from A-Z and rows from 1-100

2. Following formatting options are available ::
a) Bold , Italic and Underline
b) Font size, Font family
c) Background / Foreground color
d) Text alignment - Left , centre and Right

3. Formula : to be applied on the cell contents - The formula needs to be typed like (_A1_+_A2_),with spaces in b/w any 2 consecutive operands or operators. This is done so as to ease the parsing of the input formula.

4. document -> represents the entire browser in tree form.

5. See init.js --> here firstly we create the top row of A-Z and then the 1st column of 1-100 as column
Here there are 2 things => topRow and leftCol -> topRow is set using css property of style.css as to be on top and that of leftcol as left and then we added the values to it.When creating the string e.g. line 21 of init.js we have contentedittable = true and hence , we can edit the values inside it using the input tag 

Explain how the grid is to be created ?
It is created using first creating the elements of the topRow, wherein we created 26 columns for the column number and nested each into a div class of col and then appended this whole string into the topRow.innerHTML adding this new string values to the topRow and hence ye ek ek element uski top row mei aakar baith jaayenge and hence wo ek row ban jaayega and similarly for the left col and the grid. The whole grid has been taken to be of the 2-d array form with rows and columns and in UI also we are handling the grid in the same way using the row and column. 

The grid is basically made to be of the form of row and column id and hence jab bhi jo bhi changes karne honge hum usko refer karke hi karenge e.g. agar font change karna hai toh hum phle acquire karlenge current row and column and then document.querySelector se us element ko acquire karlenge and then el.style.fontweight = 'bold' karne se hum uska font type bold kar diya.


In script.js -> we have a fn ->
getRIdCIdfromAddress fn in script.js
Here,in what is happening is that we are converting the address to the form of row and column id e.g. if the cell is C3 then the row corresponding to it would be 3 and column id  = 2 so the cordinates are actually 3,2 .

How this font feature is actually working ?? -> line 11 -> get the element of the bold class -> this class is made inside the bui container (line 26 of index.html) and is of type button .. and so we get this button and we wil add the event listener --> line 190 --> herein we will see if it contains active-bttn --> basically this is used like when we click on the bold button then it becomes grey and this is done using the active-bttn , also we need to get the value of the row and column id from the adressBar (get address from AdressBar and then get the row and col id from getRIdCIdfromAddress function and then using the document object we will get the element of the row and col id and then we will check if the bold button is false, then add bold else remove active-bttn and bold=false). The AdressBox is a text type box . See line 68 of script.js -> whenever we click on a certain cell , an adress gets assigned to the AdressBox already and then various functions work by taking the cell name from that , get the indice of the row and column and then apply whatever functionality they want.