#ChUI.js
    
	   pO\     
	  6  /\
		/OO\
	   /OOOO\
	 /OOOOOOOO\
	((OOOOOOOO))
	 \:~=++=~:/ 
    
    ChocolateChip-UI: A framework for mobile Web app development.
    ChUI.js: The magic to make it happen.
    
    Copyright 2011 Robert Biggs: www.choclatechip-ui.com
    License: BSD
    Version 0.7 beta


$nbsp;

##Constant: UIExpectedChocolateChipJSVersion

The version that this version of ChocolateChip-UI requires. Used by UICheckChocolateChipJSVersion to check the currently loaded version of ChocolateChip.js.

&nbsp;

##Function: UICheckChocolateChipJSVersion

This method checks the currently loaded version of ChocolateChip.js and check it with the constant UIExpectedChocolateChipJSVersion. If the two are not identical, the method logs and error message to the console informing the developer which version of ChocolateChip.js this version of ChocolateChip-UI requires.

&nbsp;
  
##Variable: $.UIVersion

A variable to return the version number of ChocolateChip-UI.

**Example:**

    if (parseFloat($.UIVersion) < 0.5) {
    	alert("You need to upgrade to a newer version of ChUI.js!");
    }


&nbsp;

##Variable: $.body

This variable holds a reference to the body tag. This is a shortcut for accessing the body tag so you don't have to waste processing time getting the body tag with *$.("body")*. See below.

**Example:**

    $.body.toggleClass("portrait", "landscape");
    console.log($.body.className);


&nbsp;

##Variable: $.app

This variable holds a reference to the app tag. It is a shortcut for accessing the app tag so you don't have to waste processing time getting the body tag with *$.("app")*. See below:

**Example:**

    $.app.delegate("uibutton", "touchstart", executeMyFavFunc);


&nbsp;

##Variable: $.main

This variable holds a reference to the app's first view. This is a shortcut for accessing that view so you don't have to waste processing time getting it with *$.("#main")*. See below.

**Example:**

    $.main.UITabBar();


&nbsp;

##Variable: $.views

This variable holds a reference to all the app's views. It is a shortcut for accessing the views so you don't have to waste processing time getting them with *$$.("views")*. See below:

**Example:**

    $.views.forEach(function(view) {
        view.setAttribute("ui-navigation-status", "upcoming");
    };
    $.views[0].setAttribute("ui-navigation-status", "current");


&nbsp;

<a name="UIUuidSeed"></a>

##Function: $.UIUuidSeed

A method to generat a set of four random alpha-numeric characters. This method is used by $.UIUuid to create a uuid for use as a unique ID of elements in ChocolateChip-UI. If a seed is passed, you can force $.UIUuidSeed to generate a different number of characters. The default value that it uses is 16, which produces four characters. Passing a seed value of 20 would produce three alpha-numeric characters.

**Parameters:**

- seed: An integer used to create a set of alpha-numeric values. 

**See Also:**

[$.AlphaSeed](#AlphaSeed)

[$.UIUuid](#UIUuid)



&nbsp;

<a name="AlphaSeed"></a>

##Function: $.AlphaSeed

A method to return a random alphabetic character. This will be either lower or upper case. This method is used by $.UIUuid to create the first character of a uuid. This is necessary be by default a true uuid can begin with any alpha-numeric value. Since $.UIUuid is for creating unique IDs for elements, and IDs must beging with an alphabetic character, this method is necessary.

**See Also:**

[$.UIUuidSeed](#UIUuidSeed)

[$.UIUuid](#UIUuid)


&nbsp;

<a name="UIUuid"></a>

##Function: $.UIUuid

A method to create a uuid-like value for unique IDs on elements. This method uses $.UIUuidSeed and $.AlphaSeed to generate a uuid-like value for use as IDs. The value returned has the format: xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx. Although this is not a true uuid, the basic format and possibility of a duplicate being generated in an app are extremely unlikely.

**Example:**

    // Set a unique ID on each tablecell in the 3rd view:
    $("view:nth-of-type(3) tablecell).forEach(function(cell) {
        cell.setAttribute("id", $.UIUuid()); 
    });
    
Another useful way of identifying nodes in a collection is to use the Element.UIIdentifyChildNodes method. This identifies each node in a collection with an attribute *ui-child-position* and a numeric value indicating the nodes position in the collection.

**See Also:**

[$.AlphaSeed](#AlphaSeed)

[$.UIUuidSeed](#UIUuidSeed)

[Element.UIIdentifyChildNodes](#UIIdentifyChildNodes)



&nbsp;

<a name="UIIdentifyChildNodes"></a>

##Function: Element.UIIdentifyChildNodes

A method to identify the position of child nodes in a collection. Often you may find yourself looping through the child nodes of an element looking for which element is the one you need to change a value on based on a particular set of circumstances. To alleviate the need to loop through child nodes, ChocolateChip-UI provides this method that allows you to identify the position of child nodes with *ui-child-position* and a numeric value starting with 0. This means that you can query a child node's *ui-child-position* attribute to find out what its position is in the collection. This is especially convenient where interaction with one set of elements triggers a reaction on another set of corresponding elements, such as segmented controls and panels. By getting the *ui-child-position* value to the segmented control's segment, we can then hide or show the appropriate corresponding panel in the panel collection. It's simple to use, just execute it on the element whose child nodes you want to identify.

**Example:**

    // Number all tablecells in the tableview of view "main":
    $("#main tableview").UIIdentifyChildNodes();
    
    $("tablecell", this).bind("touchstart", function() {
        console.log("This item is at position: " + this.getAttribute("ui-child-position"));
    });

**See Also:**

[$.UIUuid](#UIUuid)



&nbsp;

<a name="UIToggleButtonLabel"></a>

##Function: Element.UIToggleButtonLabel

A method to toggle the label value of a uibutton. There are cases where when implementing a user interaction you want the button's label to toggle between two values. You might also want to toggle a class on the button or and *ui-implements* value as well. To do this you simply pass this method the two label values you wish to toggle. The first value will be the default value of the uibutton's label.

**Parameters:**

- label1: A string defining the default value for the uibutton label.
- label2: A string defining the secondary value for the uibutton label.

**Example:**

    $(toolbar + " > uibutton[ui-implements=edit]").bind("click", function() {
        if ($("label", this).text() === "Edit") {
            this.UIToggleButtonLabel("Edit", "Done");
            this.setAttribute("ui-implements", "done");
        }
    });




&nbsp;

<a name="UIButton"></a>

##Function: $.UIButton

A method to implement uibutton states for touch enabled devices. It uses an event delegate on the app tag to listen for a touchstart event on uibuttons. When one occurs, it toggles the "touched" class on the uibuttons. It uses the $.UIButtonTouched variable to know which was the most recently touched uibutton to "untouch" it. As soon as a uibutton is touched, it is cached in the $.UIButtonTouched variable.

**Syntax:**

    $.UIButton();

**See Also:**

[$.UIButtonTouched](#UIButtonTouched)


&nbsp;

<a name="UIButtonTouched"></a>

##Variable: $.UIButtonTouched

A variable to track the most recently touched uibutton. If you need to know what was the most recently touched uibutton, you can query this variable. **Note:** UIButtons in a Segmented Control have their own scheme for tracking which uibutton was touched or clicked and do not get registered with this cache.

**Example:**

    if ($.UIButtonTouched.text() == "Purchase") {
        alert("Are you sure you want to make a purchase?");
    }

**See Also:**

[$.UIButton](#UIButton)

[Element.UISegmentedControl](#UISegmentedControl)

[Element.UICreateSegmentedControl](#UICreateSegmentedControl)


&nbsp;

<a name="UINavigationHistory"></a>

##Array: UINavigationHistory

An array to store the ids of views through which the user has navigated. $.UIBackNavigation uses this to store which views the user was on and to pop them out successively for backward navigation. The default value is "#main". This means **the first view of every WAML document must have an id of #main or navigation will not work**.

**See Also:**

[$.UIBackNavigation](#UIBackNavigation)


&nbsp;
  
<a name="UIBackNavigation"></a>

##Function: $.UIBackNavigation

A method to navigate back to the previous view from whence the user came. This method uses an event delegate on the app tag to listen for clicks on all uibuttons with the attribute 'ui-implements="back"'. The method gets its destination by popping the value out of the $.UINavigationHistory array. This menu also implements page transitions by changing the ui-navigation-status of the views. The current view will always have a ui-navigation-status of "current". When navigating back, the current view's ui-navigation-status is changed to "upcoming", and the previous view's ui-navigation-status is changed to current. These changes cause the current view to transition out of view to the right and the previous view to transition into view from the left.

**Syntax:**

    $.UIBackNavigation();

**See Also:**

[$.UINavigationHistory](#UINavigationHistory)

[$.UINavigationList](#UINavigationList)


&nbsp;
  
<a name="UINavigationList"></a>

##$.UINavigationList

A method for implementing drilldown navigation for table lists. This method uses an event delegate on the app tag and listens for a click or touch on a table cell with a href attribute. When a table cell has a href attribute, this method change's that view's ui-navigation-status from "upcoming" to "current", which cause it to slide into view from the right. At the same time, it changes the current view's ui-navigation-status to "traversed", causing it to transition out of view to the left.

**See Also**

[$.UIBackNavigation](#UIBackNavigation)


&nbsp;
  
##Variable: $.UITouchedTableCell

A variable to cache the most recently touched table cell. $.UITableview uses this to toggle the touched state of table cells by add or removing the "touched" class.

##Function: $.UITableview

A method to toggle the "touched" class of table cells. This method queries the $.UITouchedTableCell to see which was the most recently touched table cell. If the cache is empty, it stores the presently touched cell and gives it the "touched" class. If the cache is not empty, it removed the "touched" class from that cell, adds the present cell to the cache and add the "touched" class to that cell.


&nbsp;

<a name="UIScrollControl"></a>

##Function: $.UIScrollControl

A method to implement scrolling of a container. This is based on iScroll by Matteo Spinelli: [cubiq.org](http://cubiq.org). Whereas his version had a lot of loose variables in the global space, ChUI.js encapsulates all variables and methods in the ChocolateChip $ object and uses ChocolateChip features where appropriate. $.UIScrollControl handles scrolling with the following private methods: handleEvent, onDOMModified, refresh, setPosition, setTransitionTime, touchStart, touchMove, touchEnd, transitionEnd, resetPosition, snap, scrollTo, scrollToPage, scrollToElement, momentum, onScrollEnd, destroy. It also uses $.UIScrollBar to create scrollbar during scrolling.

**See Also:**

[$.UIScrollBar](#UIScrollBar)

[$.UIEnableScrolling](#UIEnableScrolling)


&nbsp;
 
<a name="UIScrollBar"></a>

##Function: $.UIScrollBar

A method that creates scrollbars to indicate scrolling when an element is being scrolled. This is used by $.UIScrollControl.

**See Also:**

[$.UIScrollControl](#UIScrollControl)


&nbsp;
 
<a name="UIEnableScrolling"></a>

##Function: $.UIEnableScrolling

A method to implement automatic scrolling for all scroll panels inside of subviews. This does so by executing the $.UIEnableScrolling method on each scroll panel. This is done when the DOMContentLoaded event fires. If you dynamically create a view or subview with a scroll panel and want to implement scrolling on it, you can do so as illustrated in the example below.

**Example:**

    var opts = { desktopCompatibility: true };
    var scroller = new $.UIScrollControl($("#myNewScrollPanel", opts);

**See Also:**

[$.UIScrollControl](#UIScrollControl)


&nbsp;
 
<a name="UIDeletableTableCells"></a>

##Array: $.UIDeletableTableCells

An array of table cells chosen for deletion. This array is created and used by $.UIDeleteTableCell. As the user picks cells for deletion, they are added to this cache. 

**See Also:**

[$.UIDeleteTableCell](#UIDeleteTableCell)


&nbsp;
  
<a name="UIDeleteTableCell"></a>

##Function: $.UIDeleteTableCell

A method to enable deletion of table cells. It does this by creating an Edit and Delete uibutton which it inserts into the designated navbar or toolbar. It also creates and inserts delete indicators into each cell of the table. An event is registered on the Edit uibutton. When the user touches it, its name changes to Done and delete indicators are revealed on each table cell. If the user makes no choice and touches the Done uibutton, it hides the delete indicators and changes the Done uibutton back to the Edit uibutton. If a user does chose and item to delete and touches the Done uibutton, the delete indicators are hidden: nothing was done. If the user chooses one or more delete indicators and touches the Delete uibutton, they are deleted. The use can also select and unselect a delete indicator uibutton repeatedly touching it. By default, when the delete indicators are revealed, the Delete uibutton is disabled. As soon as the user selects a delete indicator, the Delete uibutton is enabled. But if the user deselects any selected delete indicator, the Delete uibutton will again be disabled. 

This method accepts a callback to be executed when the user has selected deletion disclosures and touches the Delete uibutton, allowing you to update whatever data is relevant to the user's choice. The method allows you to reference each deleted item through a parameter of your choice passed into the callback. For example, in the following callback, the parameter cell will automatically refer to every cell chosen for deletion:

    var handleCellDeltion = function( cell ) {
        $.deleteLocalStorage(cell.data("localStorage-key"));
    };

$.UIDeleteTableCell uses three internal function to handle its functionality: UIEditExecution, UIDeleteDisclosureSelection, UIDeletionExecution. UIEditExecution handles the user interaction with the Edit uibutton, which includes showing the deletion disclosures and Delete uibutton and changing the Edit uibutton to Done. UIDeleteDisclosureSelection handles selection and deselection of deletion disclosures, including updating the $.UIDeletableTableCells array of deletable cells, as well as enabling and disabling of the Delete uibutton. UIDeletionExecution handles deleting the cells cached in the $.UIDeletableTableCells array.

**Syntax:**

    $.UIDeleteTableCell : function(selector, toolbar, callback);

**Parameters:**

- selector: A valid CSS selector.
- toolbar: A navbar or toolbar in which to insert the Edit and Delete uibuttons.
- callback: A method to execute when the delete uibutton is touched.

**Example:**

    // Implement deletion without a callback:
    $.UIDeleteTableCell(".deletable-items1","#toolbar1");
    
    // Cell deletion with a callback:
    var deleteItem = function(item) {
        console.log("You've deleted table cell: " + item.id);
        $.deleteLocalStorage(item.id);
    };
    $.UIDeleteTableCell(".deletable-items1","#toolbar1", deleteItem);

**See Also:**

[$.UIDeletableTableCells](#UIDeletableTableCells)


&nbsp;
 
<a name="UIScreenCover"></a>

##Function: Element.UIScreenCover

A method to create a translucent cover over the screen of the browser, desktop or mobile device. It checks to see if there is not already a screen cover at this location. The screen cover is created with a ui-visible-state value of "hidden" and prevents any interaction with the covered interface. This method is used by $.UIPopUp, $.UIActionSheet, $.UIShowActionSheet, $.UIHideActionSheet.

If for some reason you wanted to cover the screen an show a custom control or message on top of it, you could do so as illustrated in the example below.

**Example:**

    $("view:first-of-type").UIScreenCover();
    $("view:first-of-type > screencover).setAttribute("ui-visible-state", "visible");

**See Also:**

[$.UIPopUp](#UIPopUp)

[$.UIActionSheet](#UIActionSheet)

[$.UIShowActionSheet](#UIShowActionSheet)

[$.UIHideActionSheet](#UIHideActionSheet)


&nbsp;
  
<a name="UIPopUpIsActive"></a>

##Variable: $.UIPopUpIsActive

A variable to keeping track of whether a popup is displayed or not. This is used by ChocolateChip-UI to know to adjust a popup on orientation change. It is a boolean value: true or false.


&nbsp;
 
<a name="UIPopUpIdentifier"></a>

##Variable: $.UIPopUpIdentifier

A variable to hold an identifier for the popup. The value is the selector indicating the parent container of the popup to distinguish it from other possible popups. This gets set by the $.UIShowPopUp method and is accessed by the $.UIPositionPopUp and $.UIRepositionPopupOnOrientationChange methods.


&nbsp;
   
<a name="UIPopUp"></a>

##Function: $.UIPopUp

A method for construction a popup. It creates both a screen cover and a popup. The popup will have a Cancel and Continue uibutton by default. Both of these will automatically close the popup. It will have a default title of "Alert!". 

**Syntax:**

    $.UIPopup(options);
    
**Parameters:**

- options: An object literal with the following possible values:
    - selector: A selector for the container into which the popup will be inserted. This allows you to have popups in different areas of your app. If no selector is supplied it defaults to the app tag.
    - title: A title for the popup to display. The default is "Alert!".
    - message: A message to display under the title. This should be some type of instruction or informative message so the user knows why the popup has appeared and what to do next.
    - cancelUIButton: An alternate name for the Cancel uibutton. It's default is Cancel.
    - continueUIButton: And alternate name for the Continue uibutton. It's default is Continue.
    - callback: A function to execute when the user touches the Continue uibutton.

**Example:**

    var myOptions = {
    selector: "#main",
    title: 'Attention Viewers!', 
    message: 'This is a message from the sponsors. Please stay seated while we are getting ready. Thank you for your patience.', 
    cancelUIButton: 'Skip', 
    continueUIButton: 'Stay tuned', 
    callback: function() {
        var popupMessageTarget = document.querySelector('#popupMessageTarget');
        popupMessageTarget.textContent = 'Thanks for staying with us a bit longer.';
        popupMessageTarget.className = "";
        popupMessageTarget.className = "animatePopupMessage";
        }
    };
    $.UIPopUp(myOptions);
    
**See Also:**

[$.UIShowPopUp](#UIShowPopUp)

[$.UIPopUpIsActive](#UIPopUpIsActive)

[$.UIPopUpIdentifier](#UIPopUpIdentifier)


&nbsp;
  
<a name="UIScreenCoverIdentifier"></a>

##Variable: $.UIScreenCoverIdentifier

A variable to identify the screen cover. This holds a reference to the screen cover in a particular parent container to distinguish it from other possible screen covers. This gets set by the $.UIShowPopUp and $.UIPositionPopUp methods.


&nbsp;

<a name="UIShowPopUp"></a>

##Function: $.UIShowPopUp

A method to show a popup. It first displays the screen cover, disabling interaction with the interface underneath, and then displays the popup. It does this by setting the ui-visible-state value of both of these to "visible". It also invokes $.UIPositionScreenCover and $.UIPositionPopUp to position the screen cover and popup on the screen properly.

**Syntax:**

    $.UIShowPopUp(selector);
    
**Parameters:**

- string: A valid selector for the parent of the tab control. This will be used to find the actual popup, which is a child node of this selector.

**Example:**

    $("#openPopup").bind("click", function() {
        $.UIShowPopUp("#main");
    });
    
**See Also:**

[$.UIPopUp](#UIPopUp)

[$.UIPositionScreenCover](#UIPositionScreenCover)

[$UIPositionPopUp](#UIPositionPopUp)

[$.UIRepositionPopupOnOrientationChange](#UIRepositionPopupOnOrientationChange)

[$.UIPopUpIsActive](#UIPopUpIsActive)

[$.UIPopUpIdentifier](#UIPopUpIdentifier)

[$.UIScreenCoverIdentifier](#UIScreenCoverIdentifier)


&nbsp;
  
<a name="UIPositionScreenCover"></a>

##Function: $.UIPositionScreenCover

 A method to make the screen cover extend the entire width of the document, even if it extends beyond the viewport. We do this by getting the window's pageYOffset in case the user has scrolled down a really long document. This method gets invoked by $.UIShowPopUp and $.UIRepositionPopupOnOrientationChange.
 
 **See Also:**
 
 [$.UIShowPopUp](#UIShowPopUp)
 
 [$.UIRepositionPopupOnOrientationChange](#UIRepositionPopupOnOrientationChange)
 

&nbsp;
 
<a name="UIPositionPopUp"></a>

##Function: $.UIPositionPopUp

A method to center the popup. It does this to the scrollview not the screen in order to accomodate the instances where the document is scrolled down below the original viewport. This gets invoked by $.UIShowPopUp and $.UIRepositionPopupOnOrientationChange.

**See Also:**

[$.UIShowPopUp](#UIShowPopUp)

[$.UIRepositionPopupOnOrientationChange](#UIRepositionPopupOnOrientationChange)


&nbsp;
 
<a name="UIRepositionPopupOnOrientationChange"></a>

##Function: $.UIRepositionPopupOnOrientationChange

A method to handle centering the popup when orientation changes or when there is a desktop window resize. It first checks $.UIPopUpIsActive and then invokes $.UIPositionScreenCover and $.UIPositionPopUp.

**See Also:**

[$.UIPopUpIsActive](#UIPopUpIsActive)

[$.UIScreenCoverIdentifier](#UIScreenCoverIdentifier)

[$.UIPositionPopUp](#UIPositionPopUp)

[$.UIPopUpIdentifier](#UIPopUpIdentifier)


&nbsp;

##Function: Element.UISelectionList

A method to initialize a list of single choice options, similar to how a group of radio butons work. It takes as the main argument, a unique selector identifying the view or section where the radio list resides. 

**Syntax:**

    $.UISelectionList(selector);
    
**Parameters:**

- function: A valid function as a callback. This is optional. The callback gets passed a reference to the clicked item, so you can access it in your callback function.

**Example:**

    $.UISelectionList("#buyerOptions");
       // Output the value of the selected item.
       // Each tablecell has its value set in the "ui-value" attribute.
       // We therefore get that value to do whater we need to do with it.
    $("#buyerOptions").UISelectionList(function(item){
		console.log(item.getAttribute("ui-value"));
	});

  
  
<a name="UICreateSwitchControl"></a>

##Function: Element.UICreateSwitchControl

A method to create a SwitchControl in a tableview cell. 

**Syntax:**

    Element.UICreateSwitchControl(options);
    
**Parameters:** 

- object literal: an object of possible values for the switch control:
    - id: and id for the switch control. and id must be supplied.
    - status: either "on" or "off", the default is "off".
    - value: any integer or string value.
    - callback: a function to execute when the switch is flipped to the "on" position.
    
**Example:**

    var opts = { 
        id : "bingo1000",
        status : "off",
        value : "$2,000",
        callback : function() {
            completeTransation(this.id);
        }
    }
    
    $("#myListItem").UIUICreateSwitchControl({
        id : "switch_001",
        status : "on",
        value : 100,
        callback : function() {
            // executeTransaction would be defined elsewhere.
            // Pass in the switch's ID to the method as a reference:
            executeTransaction(this.id);
        }
    }
    
**Note:** When using a switch control make sure that its parent container has positioning set to either relative or absolute. This is because ChocolateChip-UI uses absolute positioning to place the switch control on the right side of its container. If the container does not have some type of positioning, the switch control will appear placed somewhere towards the top right of the document. Of course, if you know the container already has positioning, you don't need to bother setting it. Tablecells already have positioning set. See example below for how to set a container's position before injecting a switch control:

    var opts = {/* options for switchcontrol */};
    // Make sure the switch control's parent has positioning set:
    $("#menu").css("{position: relative;}");
    $("#menu").UIUICreateSwitchControl(opts);
    
**See Also:**

[Element.UICreateSwitchControl](#UICreateSwitchControl)

[Element.UIInitSwitchToggling](#UIInitSwitchToggling)


&nbsp;
  
<a name="UISwitchControl"></a>;

##Function: Element.UISwitchControl

A method to toggle the state of an iPhone switch control. This also sets the state of the control's "checked" value to true or false. This value can be queried to see if it is switch is on or off. This method gets executed by the element.UIInitSwitchToggling method.

**Syntax:**

    Element.UISwitch();
   
**Example:**

    // Toggle the state of the switch control:
    $("#menu").UISwitch();

[Element.UISwitchControl](#UISwitchControl)

[Element.UIInitSwitchToggling](#UIInitSwitchToggling)


<a name="UIInitSwitchToggling"></a>

##Function: Element.UIInitSwitchToggling

A method to initialize the toggling of switch controls. By default ChococlateChip-UI call this on the app tag. If you create any switch controls dynamically, you'll need to initialize their toggling. You can invoke this method on the list that contains them. See example below.

**Syntax:**

    Element.UIInitSwitchToggling();
    
**Example:**

    $("app").UIInitSwitchToggling();
    // or:
    $$("tableview.withSwitchControls").forEach(table) {
        table.UIInitSwitchToggling();
    });
    
    
[Element.UISwitchControl](#UISwitchControl)

[Element.UICreateSwitchControl](#UICreateSwitchControl)


&nbsp;
  
<a name="UICreateSegmentedControl"></a>

##Function: Element.UICreateSegmentedControl

A method to create and insert a segmented control into a container. The segmented control consists of two or more uibuttons joined together. Both ends of the control are rounded. The segmented control can be used to execution actions or to page through several subviews. If a segmented control is inserted into a navbar or toolbar, its uibuttons will have the typical look appropriate to those bars. If the segmented control is inserted into a subview, it has a unique styling. When in a subview, you can choose to have the segmented control collapse to fit its content, or expand the width of the screen with margins on the left and right. When designating values in the options for the segmented control, values for segmented, such as to indicate a selected or disabled segment, start from 1.

**Syntax:**

    Element.UICreateSegmentedControl(options);
    
**Parameters:**

- id: an id for the segmented control
- placement: for inserting in a navbar, possible values: "left", "center", "right"
- numberOfSegments: anything from 2 on up
- titlesOfSegments: an array of titles for the segmented controls uibuttons ["One", "Two", "Three"]. If you want a segment not to have a title, put and empty string "" in its place: ["One", "", "Two"]
- iconsOfSegments: if you want to add icons to the segmented control's uibuttons enter their names here using an array. Use empty strings for uibuttons without icons: ["", "add", "info"].
- placementOfIcons: to designate the place of icons pass an array using empty strings for uibuttons were there are no icons: ["", "right", ""]. If you have designated icons without indicating their placement, they will be placed by default on the left of the uibutton label.
- selectedSegment: if you wish to designate a segment as selected, enter its position here. Possible numbers start from 1.
- disabledSegment: if you wish to designate a segment as disabled, enter its position here. Possible numbers start from 1.

**Example:**

     var seg = {
        id : "segmented_001",
        placement : "left",
        fullWidth : "false",
        numberOfSegments : 3,
        titlesOfSegments : ["One", "Two", "Three"],
        iconsOfSegments : ["", "add", "info"],
        placementOfIcons : ["", "right", ""],
        selectedSegment : 1,
        disabledSegment : 3				
	};
    $("#segmentedToolbar").UICreateSegmentedControl(seg, "first");

**See Also:**

[Element.UISegmentedControl](#UISegmentedControl)


&nbsp;
  
<a name="UISegmentedControl"></a>

##Function: Element.UISegmentedControl

A method to handle toggling of a UISegementedControl's uibuttons. This get's called during the DOMContentLoaded event so that all segmented controls have basic toggling of uibuttons. If you create a segmented control dynamically, you can call this method on it to enable toggling. See example below.

By passing an argument for a container with child nodes you can implement a segmented control that toggles the visibility of corresponding panels, similar to a tab bar. For this to work each panel must correspond to a segment. If there are more panels then segments, the segmented control will only be able to reveal the panels that numerically correspond to the number of segments. If there are more segments than panels, you will get an error. You cannot create a segmented control where some segments toggle the visibility of panels and other segments perform actions. This would be very bad usability anyway. 

**Synatx:**

    Element.UISegmentedControl(callback);
    Element.UISegmentedControl(callback, container);

**Paramters:**

- callback: A function to execute when a segmented is touched.
- container: An optional container of elements which correspond to each segment of the control.


**Example:**

    $$("segmentedcontrol").forEach(function(segmentedcontrol) {
        segmentedcontrol.UISegmentedControl();
    });    
    
    // A segmented control that toggles the child nodes of a container:
    var logChildPosition = function(item) {
        console.log("The child position is: " + item.getAttribute("ui-child-position"));
    }
    $("segmentedcontrol").UISegmentedControl(logChildPosition, "#stackpanel_1");

**See Also:**

[Element.UICreateSegmentedControl](#UICreateSegmentedControl)

[Element.UISegmentedPagingControl](#UISegmentedPagingControl)




&nbsp;

<a name="UISegmentedPagingControl"></a>

##Function: Element.UISegmentedPagingControl

A method to implement subview paging with a specialized segmented control. To create a segmented control for paging two attributes are required: *ui-implements="segmented-paging"* and *ui-paging*, which can have a value of "vertical" or "horizontal". When the *ui-paging* value is "horizontal", the segmented paging control will consist of two segmented buttons with arrows pointing left and right. When the value is "vertical", the arrows will be pointing down and up. When touching the right arrow, subviews slide in from the right. Touching the left arrow slides them out to the left. Touching the up arrow will slide subviews up from below. Touching the down arrow will slide them back down out of view. For either set, the segmented button automatically disables when there are no more subviews to navigate, leaving only the opposite direction as a choice.

This method is executed on the view whose subviews you wish to page through. It identifies the segmented control by the *ui-implements="segmented-paging"* attribute, then it identifies the subviews that it will page. Based on the value of the *ui-paging* attribute on the segmented paging control, it sets up CSS transitions for the subviews. This paging control is not like a normal segmented control or tab bar in that it can have any number of subviews to page through.

Normally you will put the segmented paging control a navbar using *ui-bar-align="right"*. When using vertical paging, subviews slide up and down underneath any navbars, toolbars or tab bars.

**See Also:**

[Element.UICreateSegmentedControl](#UICreateSegmentedControl)

[Element.UISegmentedControl](#UISegmentedControl)




&nbsp;

<a name="UICreateTabBar"></a>

##Function: Element.UICreateTabBar

A method to create a tab bar for toggling a set of subviews. Based on the values passed in as an object literal, the method constructs and tab bar and inserts it into the targeted view. The subviews that it toggles will sit between it and any top navbar or toolbar.

**Syntax:**

    var opts = {
        id : "tabbar_001",
        numberOfTabs : 5,
        imagePath : "myIcons\/",
        iconsOfTabs : ["refresh", "add", "info", "downloads", "top_rated"],
        tabLabels : ["Refresh", "Add", "Info", "Downloads", "Favorite"],
        selectedTab : 2
    };
    $("#main").UICreateTabBar(opts);


**Parameters:**

- id : a unique id for the tab bar. You could use $.UIUuid if you want or whatever id works for you.
- numberOfTabs : An integer indicating the number of tabs. Please not that on a mobile device in portrait mode the maximum number of tabs that can fit is five.
- imagePath : The path to where the tabs' icons are. This defaults to "icons/" if none is supplied.
- iconsOfTabs : And array of icon names to be used by each tab. You only need to supply the icon name, not the path or the file extension. This expects an SVG icon. By default all ChocolateChip-UI icons are stored in the "icons" folder.
- tabLabels : An array of labels that appear below the tab icons.
- selectedTab : An integer indicating a default selected state for the tab bar. By default the first tab and its subview will be selected. Numbering starts from 0. 

**See Also:**

[Element.UITabBar](#UITabBar)



&nbsp;

<a name="UITabBar"></a>

##Function: Element.UITabBar

A method for toggling a set of subviews. This method gets executed when a tab bar is created or, if you have created a tab bar manually, you can invoke it on the view where the tab bar resides. It takes no arguments but automatically finds the tab bar in the view and identifies the subviews to toggle.

**Syntax:**

    $("#main").UITabBar();

**See Also:**

[Element.UICreateTabBar](#UICreateTabBar)



&nbsp;
 
<a name="UIActionSheet"></a>

##Function: Element.UIActionSheet

Method to create an action sheet. This is a special modal control to present the user with action uibuttons to accomplish a particular task. By default the action sheet has a cancel uibutton. You may add another three uibuttons. It's recommended not to exceed four action uibuttons as it becomes difficult to access them in horizontal mode. The action sheet has a default bluish color, but you can choose to instead display it as a translucent black. 

$.UIActionSheet uses three methods internally to manage its affairs: hide(), show() and readustActionSheet(). $.UIReadjustActionSheet gets executed automatically when there is an orientation change.

**Syntax:**

    Element.UIActionSheet(options);
    
**Parameters:**

- id : an id for the action sheet.
- title : A title, such as: "This is an Annoucement!",
- color : "blue" or "black", (blue is the default).
- uibuttons : an array of uibuttons properties, each uibutton as a separate object literal:
    - [{ title : "Delete", uibuttonImplements : "delete", callback : "respondToDeleteUIButton" }, 
    - { title : "Save", uibuttonImplements : "save", callback : "respondToSaveUIButton"}]

**Example:**

    var opts = {
        id : "actionsheet_01",
        title : "This is an Annoucement!",
        color : "black",
        uibuttons : [
            { title : "Delete", uibuttonImplements : "delete", callback : "respondToDeleteUIButton" },
            { title : "Save", uibuttonImplements : "save", callback : "respondToSaveUIButton"
            }
        ]
    };
    $.body.UIActionSheet(opts);
    
    
**See Also:**

[$.UIScreenCover](#UIScreenCover)

[$.UIShowActionSheet](#UIShowActionSheet)

[$.UIHideActionSheet](#UIHideActionSheet)

[$.UIReadjustActionSheet](#UIReadjustActionSheet)


&nbsp;
  
<a name="UIShowActionSheet"></a>

##Function: $.UIShowActionSheet

A method to show an action sheet. When this method show an action sheet, it also stores a special attribute on the app tag "ui-action-sheet-id" to store the id of the displayed action sheet. This value is used by UIReadjustActionSheet when the device orientation changes to know which action sheet is presently displayed.

**Syntax:**

    $.UIShowActionSheet(id);
  
**Parameters:**

- id: a valid id for an action sheet.

**Example:**

    $("#UIButtonAction").bind("touchstart", function() {
        $.UIShowActionSheet(actionsheet_01);
    });

**See Also:**

[$.UIHideActionSheet](#UIHideActionSheet)

[$.UIReadjustActionSheet](#UIReadjustActionSheet)


&nbsp;
 
<a name="UIHideActionSheet"></a>

##Function: $.UIHideActionSheet

A method to hide an action sheet. This method also removes the id of the action sheet being hidden from the app tag's "ui-action-sheet-id" attribute. This method get executed automatically by the action sheet's Cancel uibutton.

**Syntax:**

    $.UIHideActionSheet(id);
    
**Parameters:**

- id: a valid id for an action sheet.

**Example:**

    $("#displayActionSheet").bind("click", function() {
        $.UIShowActionSheet("#Dingo");
    });


**See Also:**

[$.UIShowActionSheet](#UIShowActionSheet)

[$.UIReadjustActionSheet](#UIReadjustActionSheet)


&nbsp;
  
<a name="UIReadjustActionSheet"></a>

##Function: $.UIReadjustActionSheet

A method to readjust the positioning of an action sheet after orientation change. You never need to use this function.


**Example:**

    document.addEventListener("orientationchange", function() {
        $.UIReadjustActionSheet();
    });

**See Also:**

[$.UIShowActionSheet](#UIShowActionSheet)

[$.UIHideActionSheet](#UIHideActionSheet)


##Function: $.UIAdjustToolBarTitle

A method to adjust the length of a title in a navbar. This method is execute when DOMContentLoad, onorientationchage and window.resize occur. It check the navbar for the title's siblings, calculates their widths and determines, based on the current width of the navbar, how much space is left for the title. It then adjust the width of the title. By default the navbar's title has a text-overflow value of ellipsis, so when the width of the title is less than the content, the text gets truncated and replaced with an ellipsis. When there is just enough room for only one character and an ellipsis, the method hides the title completely.

**Syntax:**

    $.UIAdjustToolBarTitle();
    
**Example:**

    $.UIAdjustToolBarTitle();


&nbsp;
 
<a name="UIActivityIndicator"></a>

##Function: $.UIActivityIndicator

Method to create an activity indicator using the canvas element. This method is just an empty constructor for the activity indicator. It's sub-methods handle creation, animation and deletion of the activity indicator.

[$.UIActivityIndicator.create](#UIActivityIndicator_create)

[$.UIActivityIndicator.animate](#UIActivityIndicator_animate)

[$.UIActivityIndicator.stop](#UIActivityIndicator_stop)

[Element.UIInsertActivityIndicator](#UIInsertActivityIndicator)


&nbsp;
  
<a name="UIActivityIndicator_create"></a>

##Function: $.UIActivityIndicator.create

This is created dynamically and redrawn on the background of the designated container. It will spin continuously until the $.UIActivityIndicator.stop() method is executed.

A function to create an activity indicator. It takes an object literal of values to create the activity indicator. By default it draws the activity indicator as a background image on an element of the designated container. If no container is designated, the method will try to output it to a container with the class "UIActivityIndicator", which is already defined in ChUI.css to display a canvas background image.

**Syntax:**

    $.UIActivityIndicator.create(options);

**Parameters:**

- id: a unique id for the activity indicator. If no id is supplied, it defaults to "UIActivityIndicator."
- color: a hexidecimal or rgb/rgba value for the color of the tines of the activity indicator. If no value is supplied it defaults to "gray."
- shadow: a hexicdecimal or rgb/rgba value for the color of shadow for the tines of the activity indicator. If no value is supplied, the activity indicator will be drawn without any shadow.
- container: a selector indicating the container in which to draw the activity indicator. If no selector is supplied it defaults of the class "UIActivityIndicator". You can add this class dynamically to an element in which you wish to display an activity indicator. **Note:** If you output an activity indicator on a container that already has a background image of type image or gradient, this will be replaced by the activity indicator. So, depending on where you want to show the activity indicator, you may need to inject a new element into the desired area to show the activity indicator if you don't want the main area's background image to be replaced by the activity indicator.
- size: the size for the activity indicator. This can be pixels or percent. If no size is passed, it defaults to 75%. This gets output as the background size for the render canvas image. **Note:** If you set a size for the activity indicator, make sure that the element you are outputting it in is big enough to display it.

**Example:**
    
    var opts = {
        id : "activityIndicator_01",
        color : #666,
        shadow : #ccc,
        container : ".ajaxUpdateInProgress"
    }
    var activityIndicator = new $.UIActivityIndicator.create(opts);

[$.UIActivityIndicator](#UIActivityIndicator)

[$.UIActivityIndicator.animate](#UIActivityIndicator_animate)

[$.UIActivityIndicator.stop](#UIActivityIndicator_stop)


&nbsp;
  
<a name="UIActivityIndicator_animate"></a>

##Function: $.UIActivityIndicator.animate

A method to animate an activity indicator. Before invoking it you need a pointer to an activity indicator (see example below).  This method redraws the activity indicate at intervals of 100 milliseconds.

**Syntax:**

    $.UIActivityIndicator.animate()
    
**Example:**

    var activityIndicator = new $.UIActivityIndicator.create(opts);
    activityIndicator.animate();

[$.UIActivityIndicator](#UIActivityIndicator)

[$.UIActivityIndicator.create](#UIActivityIndicator_create)

[$,UIActivityIndicator.stop](#UIActivityIndicator_stop)


&nbsp;
  
<a name="UIActivityIndicator_stop"></a>

##Function: $.UIActivityIndicator.stop

A method to stop the animation of an activity indicator.

**Syntax:**

    $.UIActivityIndicator.stop()

**Example:**

    var activityIndicator = new $.UIActivityIndicator.create(opts);
    activityIndicator.animate();
    // Set a delay for when to stop the activity indicator:
    $.delay(activityIndicator.stop(), 2000);

[$.UIActivityIndicator](#UIActivityIndicator)

[$.UIActivityIndicator.create](#UIActivityIndicator_create)

[$.UIActivityIndicator.animate](#UIActivityIndicator_animate)


&nbsp;

<a name="UIInsertActivityIndicator"></a>

##Function: Element.UIInsertActivityIndicator

To make it easier to implement an activity indicator with the previously defined methods, ChocolateChip-UI provides Element.UIInsertActivityIndicator. This allows you to pass the options you want for an activity indicator and inserts it in a panel container inside of an element. It also allows you to pass an optional style declaration that gets inserted inline on the activity indicator's panel. This allows you to insert and activity indicator where you need one, in a navbar, toolbar or subview, without worrying about the background canvas image wiping out the background on the parent container. If you were going to use this with an Ajax call, you could first insert the activity indicator into the place where the content will be placed. Then as part of the Ajax call's successCallback function, remove the activity indicator and insert the content. Please refer to Element.xhr in the documentation for ChocolateChip.js for more details about how to do Ajax calls with ChocolateChip-UI.

When using this method there is no need to invoke $.UIActivityIndicator.init, $.UIActivityIndicator.animate or $.UIActivityIndicator.stop. The animation begins as soon as the activity indicator is inserted. It is stopped by you removing it when there is a success or error returned by the Ajax call. See example below.

**Example:**

	var content = $("#content");
	// First insert an activity indicator:
	content.UIInsertActivityIndicator({
		id: "activity_indicator_01", 
		color: "#fff",
		container: "navbar > panel",
		size: "40px",
		style : "margin: 40px auto 0 auto;"
	});
    // Then make the Ajax call:
	content.xhr("data.html", {
		successCallback: function() {
            // If the call is successful, empty the
            // container to get rid of the activity indicator:
            content.empty();
			content.insert($.responseText);
			$.responseText = null;
			content.after($.make("<h2>Ajax call was successful.</h2>"));
		},
		errorCallback: function() {
            // If there was an error, remove activity indicator:
            content.empty();
			content.insert("There was an error getting the file.");
		}
	});


&nbsp;
  
<a name="UISlider"></a>

##Function: $.UISlider

A method to initialize a horizontal slider with thumb. This supports both touch and mouse interaction. This is useful for allowing the user to choose a value from a sliding range of possible values. This method creates two variables on the ChocolateChip object: UICurX and UICurY. These are the current x and y coordinates of the mouse or touch. It also adds the "ui-slider-length" attribute to the slider to store its clientWidth for use by the various functions for calculating drag coordinates for moving the slider thumb.

$.UISlider checks for touch support to determine which way to track dragging of the slider thumb. When it is touch-based, it invokes element.UISliderTouch and element.UIUpdateSliderTouch. When it is mouse-based it invokes $.UISliderForMouse, which initializes various functions for mouse interaction. Although this method is executed on a selector for a slider, the method listens for drag events on the slider's thumb. For mouse interaction it provides to ways to manage dragging with onDrag and onDragEnd as possible values passed in as options. For the slider to work properly you need to output the width you desire for the slider directly on it using an inline style setting, such as: *style="width: 186px;"*. This allows you to give each slider a different width depending on your needs. ChocolateChip-UI's methods will query this assigned width and use it for dragging the thumb and updating the slider's progress track. See examples below. 

The method expects the following WAML markup to function:

**Markup:**

    <slider id="slider_001" style="width: 180px;">
        <thumb><thumbprop></thumbprop></thumb>
    </slider>

Or an optional class of "media-player" for a metallic look:
    
    <slider id="slider_002" class="media-player" style="width: 200px;">
        <thumb><thumbprop></thumbprop></thumb>
    </slider>
    
**Syntax:**

    $.UISlider(selector, options);

**Parameters:**

- selector: a selector identifying the slider.
- options: an object literal of possible values for the slider:
    - 
    
**Example:**

    var updateColorFromSlider = function() {
        // Code here to execute.
    }
    $.UISlider("#redSlider", { callback: updateColorFromSlider });


**See Also:**

[$.UIDrag.init](#UIDrag_init)

[Element.UISliderTouch](#UISliderTouch)

[Element.UIUpdateSliderTouch](#UIUpdateSliderTouch)

[$.UISliderForMouse](#UISliderForMouse)

[$.UISliderValue](#UISliderValue)


&nbsp;
 
<a name="UICurX"></a>

##Variable: $.UICurX

This is a variable that keeps track of the x coordinate of a mouse or touch move. It's default value is null. This variable gets used by $.UISlider, Element.UISliderTouch, Element.UIUpdateSliderTouch and $.UIDrag.

**See Also:**

[Element.UISliderTouch](#UISliderTouch)

[Element.UIUpdateSliderTouch](#UIUpdateSliderTouch)

[$.UIDrag](#UIDrag)

[$.UISliderValue](#UISliderValue)


&nbsp;
  
<a name="UICurY"></a>

##Variable: $.UICurY

This is a variable that keeps track of the y coordinate of a mouse or touch move. It's default value is null. This variable is used to determine the constant y coordinate for the slider thumb while it is being dragged.

**See Also:**

[$.UICurX](#UICurX)

[$.UISliderValue](#UISliderValue)

[$.UIDrag](#UIDrag)


&nbsp;
  
<a name="UISliderValue"></a>

##Variable: $.UISliderValue

This is a variable that keeps track of the value of the drag subtracting the thumb width from the slider length. This is the value you would need to read to do something with when the user drags the slider's thumb. In contrast, $.UICurX and $.UICurY are used from tracking the positioning of the thumb and slider progress track.


&nbsp;
  
<a name="UISliderTouch"></a>

##Function: Element.UISliderTouch

Method to calculate the value of the user's finger for updating the left position of the slider thumb and length of the slider's track progress bar. By accessing the ui-slider-length property of the slider, the method calculates the current touch position and stores it in the $.UICurX, which will be used by element.UIUpdateSliderTouch to calculatethe position of the slider thumb and the slider track progress indicator. This method gets called by $.UISlider.

**See Also:**

[$.UICurX](#UICurX)

[$.UISliderValue](#UISliderValue)

[$.UISlider](#UISlider)


&nbsp;
 
<a name="UIUpdateSliderTouch"></a>

##Function: Element.UIUpdateSliderTouch

Method to update the thumb position and length of the left track progress indicator when the user drags a slider thumb horizontally. The method gets the length of the slider and calculates the distances based on this.

**Syntax:**


**Parameters:**

- callback: a function to execute while the thumb is dragged and updates the track progress indicate by accessing the $.UICurX value.

**See Also:**

[$.UICurX](#UICurX)

[$.UISliderValue](#UISliderValue)

[$.UISlider](#UISlider)

[$.UISliderForMouse](#UISliderForMouse)


&nbsp;
 
<a name="UIDrag"></a>

##Function: $.UIDrag

A method that holds a number of properties and functions to handle mouse-based dragging. Its members are: obj (the object being dragged), init (setup for dragging), start (executed when a drag begins), end (executed when a drag ends), fixE (resolves calculating the x and y coordinates) and updateSliderProgressIndicator (updates the track progress indicator as the slider's thumb is dragged).

**See Also:**

[$.UIDrag.init](#UIDrag_init)

[$.UICurX](#UICurX)

[$.UICurY](#UICurY)

[$.UISliderValue](#UISliderValue)


&nbsp;
  
<a name="UIDrag_init"></a>

##Function: $.UIDrag.init

A method to step up mouse-based dragging. It automatically initializes the slider's thumb for dragability. Its parameters are derived automatically from the selector, the slider's thumb, the slider's length and several predefined values.

**See Also:**

[$.UIDrag](#UIDrag)

[$.UISliderForMouse](#UISliderForMouse)


&nbsp;
 
<a name="UISliderForMouse"></a>

##Function: $.UISliderForMouse

Method to initialize a range slider for mouse interaction. This gets invoke the $.UISlider. It uses $.UIDrag.init to set the slider for mouse dragging. It will also execute any callback passed to $.UISlider. It receives all of its parameters from $.UISlider.

**Syntax:**

    $.UISliderForMouse(selector, options);

**Parameters:**

- selector: a selector identifying the slider.
- options: an object literal of possible values for the slider:

**See Also:**

[$.UISlider](#UISlider)

[$.UIDrag.init](#UIDrag_init)

[$.UISliderValue](#UISliderValue)




&nbsp;

<a name="UISetTranstionType"></a>

##Function: Element.UISetTranstionType

A method to set the type of transition for toggling between two subviews. Possible transitions are flip, pop, fade and spin. Depending on the type of transition, it sets up the appropriate CSS on the view so that the subviews can transition properly. This gets invoked automatically by element.UIFlipSubview, element.UIPopSubview, element.UIFadeSubview. and element.UISpinSubview.

**Parameters:**

- flip: 
- pop: 
- fade: 
- spin: 

**See Also:**

[Element.UIFipSubview](#UIFipSubview)

[Element.UIPopSubview](#UIPopSubview)

[Element.UIFadeSubview](#UIFadeSubview)

[Element.UISpinSubview](#UISpinSubview)



&nbsp;

<a name="UIFipSubview"></a>

##Function: Element.UIFipSubview

A method for flipping over a subview to reveal another subview, like flipping a card over to see its back. The method toggles a pair of classes to trigger the different transitions between the two subviews. To implement this flipping of subviews, bind this to the uibutton or other element you want to trigger the action.

**Parameters:**

- right: Flips the subview over to the right to reveal another subview as its back.
- left: Flips the subview over to the left to reveal another subview as its back.
- top: Flips the subview upwards to reveal another subview as its back.
- bottom: Flips the subview downwards to reveal another subview as its back.

**Syntax:**

    Element.UIFlipSubview(direction);

**Example:**

    $("#flipbutton").UIFlipSubview("bottom");

**See Also:**

[Element.UISetTranstionType](#UISetTranstionType)

[Element.UIPopSubview](#UIPopSubview)

[Element.UIFadeSubview](#UIFadeSubview)

[Element.UISpinSubview](UISpinSubview)



&nbsp;

<a name="UIPopSubview"></a>

##Function: Element.UIPopSubview

A method for popping up or popping out a subview over the current subview. The method toggles a pair of classes to trigger the different transitions between the two subviews. To implement this popping of subviews, bind this to the uibutton or other element you want to trigger the action.

**Syntax:**

    Element.UIPopSubview();

**Example:**

    $("#popbutton").UIPopSubview();

**See Also:**

[Element.UISetTranstionType](#UISetTranstionType)

[Element.UIFipSubview](#UIFipSubview)

[Element.UIFadeSubview](#UIFadeSubview)

[Element.UISpinSubview](#UISpinSubview)




&nbsp;

<a name="UIFadeSubview"></a>

##Function: Element.UIFadeSubview

A method to implement the fading in and out of a secondary subview. The method toggles a pair of classes to trigger the different transitions between the two subviews. To implement this fading of subviews, bind this to the uibutton or other element you want to trigger the action.

**Syntax:**

    Element.UIFadeSubview();

**Example:**

    $("#fadebutton").UIFadeSubview();

**See Also:**

[Element.UISetTranstionType](#UISetTranstionType)

[Element.UIFipSubview](#UIFipSubview)

[Element.UIPopSubview](#UIPopSubview)

[Element.UISpinSubview](#UISpinSubview)



&nbsp;

<a name="UISpinSubview"></a>

##Function: Element.UISpinSubview

A method to spin in and out a secondary subview. The method toggles a pair of classes to trigger the different transitions between the two subviews. To implement this spinning of subviews, bind this to the uibutton or other element you want to trigger the action.

**Syntax:**

    Element.UISpinSubview(direction);
    
**Parameters:**

- left: Will spin the subview in clockwise.
- right: Will spin the subview in counterclockwise.

**Example:**

    $("#spinbutton").UISpinSubview("left");

**See Also:**

[Element.UISetTranstionType](#UISetTranstionType)

[Element.UIFipSubview](#UIFipSubview)

[Element.UIPopSubview](#UIPopSubview)

[Element.UIFadeSubview](#UIFadeSubview)