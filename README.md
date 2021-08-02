Js code cannot run independently . It needs to be called either inside the browser or via an env and hence we have mentioned all the scripts as < script >  script_name < / script >

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


How to have the toolbar in sync  -> everything in script.js -> e.g. see 166-167 -> if one is active dull the rest ==>  like this many are going on

Dual binding has been implemented here--->  whenever we click on any cell the toolbaar experience changes accordingly (if value inside is bold,then bold becomes black and so on) and whenever we click on any of the toolbar options, then the effect is seen on the cell values and hence this is known as dual binding.{The effect of changes on the toolbar is seen on the elements of the grid as jab humne grid element pe click kiya .. address bar got the value, the toolbar will get the adress of the cell , i.e. the actual cell and accordingly perform the operations using the document API by gathering its rows and columns.}




   FLOW OF THE PROJECT :::::

   1. Construct a grid in the init.js with initialising the columns , rows and then the grid cell elements.
   2. Achieve the functionality of filling the adress bar with the adress of the given cell we have clicked upon.
   3. Consider each object of the 2d array as a cell as a object 
   4. Then we added the functionalities of all the elements one by one .. In script.js we have initially at the start obtained the objects of all the functionalities of the toolbar using the document API , so as to apply the required changes over them.
   5. Then we implement dual binding i.e. affect of functioning on toolbar is seen and vice-versa of cells on toolbar.
   6. After that we will implement the formula.

   FORMULA -->

   1. The value of cell is defined by the given formula, if a3 is used to define the value of a4 , then change in a3 will lead to change in the value of a4 and if we change the value of a4 ourselves, then a3 would stop affecting the value of a4.
   2. Constraints ::: we can only set the formula in the formula bar .  There are only 26 columns and 1-100 rows.
   3. Every token of the formula must be space separated.
   In the formula, there is associated , formula and children array with all of the cells present. Now, if we want to apply a formula, the formula gets added to the cell and as well as the children and then we simply change the children value using the formula. Now, if the value of any children gets changed, what we do is that since we have the formula with us, so we will go the parents(parsing the formula present ) and then remove the cell  from their children array and also the formula of the cell will be replaced by the new value and the formula and corresponding children will be removed from the parent of the changed cell.
   4. Cycle detection a2->2*a1 , b1->2*a1 and a2->2*b1 =>cycle  => test it first 
   5. Also we need to check at the start that whether the formula syntax is valid or not.


Now, when we have to enter the formulae, what we do is to type the formula and then press enter, which means, ENTER is the symbol that the formula has been written and we want the current cell to be updated by that particular value of the output of the formulae. SEE Line 298 -> So when we press a enter key and formula is present, we will check if prev formula was not null then we will remove it and then evaluate the new formula { using the evaluate function which will simply first split the string and then for each of the values e.g. A1 OR B3 etc. get the value present at those point and then replace these values inside the formula and then call the eval function which will automatically (inbuilt function) give the result values} . Now, set the current value of this cell as the evaluated result. 

