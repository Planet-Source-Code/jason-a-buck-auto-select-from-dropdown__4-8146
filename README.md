<div align="center">

## Auto Select from Dropdown


</div>

### Description

Allows you to select an item from a DROP DOWN by typing in more than just the first letter.
 
### More Info
 
A drop down list with the item you typed selected if it is in the list.


<span>             |<span>
---                |---
**Submitted On**   |
**By**             |[Jason A Buck](https://github.com/Planet-Source-Code/PSCIndex/blob/master/ByAuthor/jason-a-buck.md)
**Level**          |Advanced
**User Rating**    |4.0 (16 globes from 4 users)
**Compatibility**  |ASP \(Active Server Pages\), HTML, VbScript \(browser/client side\)

**Category**       |[ASP Server Object Model](https://github.com/Planet-Source-Code/PSCIndex/blob/master/ByCategory/asp-server-object-model__4-32.md)
**World**          |[ASP / VbScript](https://github.com/Planet-Source-Code/PSCIndex/blob/master/ByWorld/asp-vbscript.md)
**Archive File**   |[](https://github.com/Planet-Source-Code/jason-a-buck-auto-select-from-dropdown__4-8146/archive/master.zip)

### API Declarations

Not done by me, done by Mike Pope, no contact information available


### Source Code

```
<html>
	<head>
		<title></title>
				<SCRIPT language=javascript>
				// thanks to GOOD OLE MICROSOFT, I can provide you the following working
				// example of a DROP DOWN LIST that allows you to type more than the
				// FIRST LETTER of what you are looking for in a drop down.
				// I hopw that you find this to be useful. I have been looking for this
				// code for almost a year now.
				// Again, do not vote for me as this code is from Microsoft.
				// Respectfully, Jason Buck jbuck@esubinc.com
				// Happy Programming.
				// The CODE WAS FOUND at the following location
				// http://msdn.microsoft.com/msdnmag/issues/01/05/web/figures.asp
// Auto-select listbox
// mike pope, Visual Basic UE
// This script and the listbox on this page illustrates one
// way to create an "auto-complete" listbox, where the
var toFind = "";       // Variable that acts as keyboard buffer
var timeoutID = "";      // Process id for timer (used when stopping
               // the timeout)
timeoutInterval = 250;    // Milliseconds. Shorten to cause keyboard
               // buffer to be cleared faster
var timeoutCtr = 0;      // Initialization of timer count down
var timeoutCtrLimit = 3 ;   // Number of times to allow timer to count
               // down
var oControl = "";      // Maintains a global reference to the
               // control that the user is working with.
function listbox_onkeypress(){
  // This function is called when the user presses a key while focus is in
  // the listbox. It maintains the keyboard buffer.
  // Each time the user presses a key, the timer is restarted.
  // First, stop the previous timer; this function will restart it.
  window.clearInterval(timeoutID)
  // Which control raised the event? We'll need to know which control to
  // set the selection in.
  oControl = window.event.srcElement;
  var keycode = window.event.keyCode;
  if(keycode >= 32 ){
    // What character did the user type?
    var c = String.fromCharCode(keycode);
    c = c.toUpperCase();
    // Convert it to uppercase so that comparisons don't fail
    toFind += c ; // Add to the keyboard buffer
    find();  // Search the listbox
    timeoutID = window.setInterval("idle()", timeoutInterval);
    // Restart the timer
  }
}
function listbox_onblur(){
  // This function is called when the user leaves the listbox.
  window.clearInterval(timeoutID);
  resetToFind();
}
function idle(){
  // This function is called if the timeout expires. If this is the
  // third (by default) time that the idle function has been called,
  // it stops the timer and clears the keyboard buffer
  timeoutCtr += 1
  if(timeoutCtr > timeoutCtrLimit){
   resetToFind();
   timeoutCtr = 0;
   window.clearInterval(timeoutID);
  }
}
function resetToFind(){
  toFind = ""
}
function find(){
  // Walk through the select list looking for a match
  var allOptions = document.all.item(oControl.id);
  for (i=0; i < allOptions.length; i++){
    // Gets the next item from the listbox
    nextOptionText = allOptions(i).text.toUpperCase();
    // By default, the values in the listbox and as entered by the
    // user are strings. This causes a string comparison to be made,
    // which is not correct for numbers (1 < 11 < 2).
    // The following lines coerce numbers into an (internal) number
    // format so that the subsequent comparison is done as a
    // number (1 < 2 < 11).
    if(!isNaN(nextOptionText) && !isNaN(toFind) ){
       nextOptionText *= 1;    // coerce into number
       toFind *= 1;
    }
    // Does the next item match exactly what the user typed?
    if(toFind == nextOptionText){
      // OK, we can stop at this option. Set focus here
      oControl.selectedIndex = i;
      window.event.returnValue = false;
      break;
    }
    // If the string does not match exactly, find which two entries
    // it should be between.
    if(i < allOptions.length-1){
      // If we are not yet at the last listbox item, see if the
      // search string comes between the current entry and the next
      // one. If so, place the selection there.
      lookAheadOptionText = allOptions(i+1).text.toUpperCase() ;
      if( (toFind > nextOptionText) &&
       (toFind < lookAheadOptionText) ){
       oControl.selectedIndex = i+1;
       window.event.cancelBubble = true;
        window.event.returnValue = false;
       break;
      } // if
      } // if
    else{
      // If we are at the end of the entries and the search string
      // is still higher than the entries, select the last entry
      if(toFind > nextOptionText){
        oControl.selectedIndex = allOptions.length-1 // stick it
                              // at the end
        window.event.cancelBubble = true;
        window.event.returnValue = false;
        break;
      } // if
    } // else
  } // for
} // function
</SCRIPT>
	</head>
	<body>
				<select name="FontList" ID="Select1"  onkeypress="listbox_onkeypress()" onblur="listbox_onblur()">
			<option id="arial" value="arial">Arial</option>
 <option id="arial black" value="arial black">Arial black</option>
 <option id="arial narrow"value="arial narrow">Arial narrow</option>
 <option id="bookman" value="Bookman">Bookman</option>
 <option id="book antiqua" value="book antiqua">Book Antiqua</option>
 <option id="bookman old style" value="bookman old style">Bookman Old Style</option>
 <option id="century gothic" value="century gothic">Century Gothic</option>
 <option id="comic sans ms" value="comic sans ms">Comic Sans MS</option>
 <option id="courier" value="courier">Courier</option>
 <option id="courier new" value="courier new">Courier New</option>
 <option id="garamond" value="garamond">Garamond</option>
 <option id="georgia" value="georgia">Georgia</option>
 <option id="haettenschweiler" value="haettenschweiler">Haettenschweiler</option>
 <option id="helvetica" value="helvetica">Helvetica</option>
 <option id="impact" value="impact">Impact</option>
 <option id="lucida console" value="Lucida Console">Lucida</option>
 <option id="lucida sans unicode" value="Lucida Sans Unicode">Lucida Sans Unicode</option>
 <option id="marlett" value="Marlett">Marlett</option>
 <option id="microsoft sans serif" value="Microsoft Sans Serif">Microsoft Sans Serif</option>
 <option id="monotype corsiva" value="Monotype Corsiva">Monotype Corsiva</option>
 <option id="ms outlook" value="MS Outlook">MS Outlook</option>
 <option id="newcenturyschlbk" value="NewCenturySchlbk">NewCenturySchlbk</option>
 <option id="palatino" value="Palatino">Palatino</option>
 <option id="palatino linotype" value="Palatino Linotype">Palatino Linotype</option>
 <option id="symbol" value="Symbol">Symbol</option>
 <option id="tahoma" value="Tahoma">Tahoma</option>
 <option id="times" value="Times">Times</option>
 <option id="times new roman" value="Times New Roman">Times New Roman</option>
 <option id="trebuchet ms" value="Trebuchet MS">Trebuchet MS</option>
 <option id="verdana" value="Verdana">Verdana</option>
			</select>
	</body>
</html>
```

