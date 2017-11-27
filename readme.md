# Dynamic-popup-form #

This is module to create dynamic dialog form which asking user for data. Now allowed text input, file input, textarea, select and label text. It is completely independent and don't require depencencies neither on frameworks nor libraryes.

# Using in browser #

To use in browser just add dynamic-popup-form.js with ```<script>``` tag and dynamic-popup-form.css in ```<style>``` tag. 

# Using with bundlers (Webpack, Rollup etc) #

I didn't try yet, but i suppose this can work.

# Styles #

All styles containing in file dynamic-popup-form.css. This is for convient to customize. You can edit this styles, bundle it etc.

# Documentation #


Dynamic Popup Form Dialog is created be class PopupForm with particular parameters. These parameters is a object, containing description needed to create dialog. Method 'show' show the created dialog. Dialog window have two buttons 'Ok' and 'Cancel'. Object parameters have to provide two methods to deal with user choise. One method is invoked when user clicks 'Ok' and second method is invoked when user clicks 'cancel'. 


~~~
	var params = 
	{
		'type': 'label', 
		value: 'You really want to destroy this?', 
		handler: function (value) 
		{
			Destroy();
		}
	};


	var form = new PopupForm(params);
	form.show();
~~~

### Input types ###
    
Object params have to contain some keys.

+ type - type of html input DOM element. Now following types is accepted:
* label - will be created ```<label>``` html element. This is convieced for confirmation dialogs.
* text - will be created ```<input type='text'>``` element.
* file - will be created ```<input type="file">``` element.

### Select ###

select - will be created ```<select>``` element.

Initial values must be in 'value' key:


Creating dialog containing text label and two buttons 'Ok' and 'Cance'.

~~~
var params
{
    'type': 'label',
    'value': 'Some text?'
}
~~~

Creating dialog with text input field

~~~
var params
{
    'type': 'text',
    'value': 'Some text'
}
~~~

Creating dialog with text textarea

~~~
var params
{
    'type': 'textarea',
    'value': 'Some text'
}
~~~


When 'type' is 'select' you have to provide set of option in 'options' key. This key can be either array or object. Keys of object set attribute 'value' of 'option' html element. Values set text in option html element. Key 'value' can contain initial selected element. 

This parameters

~~~
var params 
{
    'type': 'select',
    'options': {
        'option value 1': 'option name 1',
        'option value 2': 'option name 2'
    },
    value: 'option name 1',
}
~~~

result in:

~~~
<select>
<option value="option value 1" selected>option name 1</option>
<option value="option value 2">option name 2</option>
</select>
~~~

Or can use array. Then option value and option text will be same.
~~~
var params 
{
    'type': 'select',
    'options': [
        'option 1', 'option 2'
    ],
    value: 'option 1'
}

<select>
<option value="option 1" selected>option 1</option>
<option value="option 2">option 2</option>
</select>

~~~

### List of fields ###

There is can use list of fields if one fields is not enough. Descriptions of fields are set in key 'fields'. It is array of object like this:

~~~
var params {
    fields : [
        {
        type: select,
        options : 
            {
                "one": "1",
                "two": "2"
            }
        value: "1"
        "data-value": "tag"
        },
        {
            type: text,
            "data-value": "comment"
        }
    ],
    handler : function (value) {
        console.log(JSON.stringify(value));
    }
}
~~~

This print some like

~~~
{ 
    "tag": "1",
    "comment": "some text"
}
~~~

Each object in 'fields' array contain keys - type, value, options, etc, which is need to field of this type. Argument 'value' passed in 'handler' contain object, where keys are 'data-value' value. 