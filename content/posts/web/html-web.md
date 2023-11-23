+++
title = 'Web technologies - basic HTML/CSS/JS'
date = 2023-11-17T09:21:22+05:30
draft = false
+++

# Web notes

## FYI
- CSA: Client server architecture
- A web can be two tier, three tier, n tier having different applets for different purposes
- HTML: Hypertext markup lang, CSS: Cascading stylesheet, JS: Javascript
- P2P: Peer to peer architecture
- DOM: Document Object Model (DOM) is a file model wherein all the files are shown in a multiinterface structural model
- Tree stucture: A tree structure is a model where the start point is a single node but as we go down the model the number of nodess increase just like a tree.

## Misc
- &npsp: singlewhitespace

## Basics
### Structure of a HTML document
A HTML document contents many tags called as elements. These elements are crutial in making a HTML document. This is the common structure of an HTML document.
```html
<!DOCTYPE html>
<head>
	<!-- your head details -->
</head>
<body>
	<!-- your body details -->
</body>
</html>
```
HTML is completely independent to indentations for standard webpages.

### Comments
A comment is a non executable piece of code that can be added to the code to make it more readable for the devloper. A comment in HTML can be made like this
```html
<!--  -->
```
### Adding simple text
This section contains the following
1. Adding headings
2. Adding paragraph
3. Simple text formatting - bold, italic, underline
```html
<!DOCTYPE html>
<html lang="en">
<head>
</head>
<body>
	<!-- Adding heading to the code -->
	<h1>Hello world</h1>
	<!-- Text formatting -->
	<!-- b: bold; i: italics; u: underline -->
	<p> <b>This </b>is <i>a </i>simply simply <u>lovleh </u>paragraph</p>
	<p>Example for the<br>use of linebreak</p>
</body>
</html>
```

### Adding heading detais
1. Adding title
2. Adding icons to tabs
3. Adding CSS extention to main document
```html
<!DOCTYPE html>
<html lang="en">
<head>
	<!-- Tab title -->
	<title>First webpage</title>
	<!-- Link to CSS -->
	<link rel="stylesheet" href="style.css">
	<!-- Web icon -->
	<link rel="icon" href="icon.png">
</head>
<body>
</body>
</html>
```

### Styling in another way
There are two methods of using CSS in HTML 5. One method is to use a seperate CSS document that contents all the styling attributes, another method is to include a style tag and include all the styling attributes inside the styling tab.

- Within HTML (head section)
```html
<!DOCTYPE html>
<html lang="en">
	<style>
		body {
			background: #e71515;
		}
		h1 {
			color: #ffffff;
		}
	</style>
<head>
	<title>Styling guide</title>
</head>
<body>
	<h1>This is a document</h1>
</body>
</html>
```

- Using HTML and CSS (external way)\
Contents of HTML document
```html
<!DOCTYPE html>
<html lang="en">
<head>
	<link rel="stylesheet" href="style.css">
	<title>Styling guide</title>
</head>
<body>
	<h1>This is a document</h1>
</body>
</html>
```
Contents of CSS document
```css
body {
	background: #e71515;
}
h1 {
	color: #ffffff;
}
```

- Inline use of stylesheets
```html
<!DOCTYPE html>
<html lang="en">
<head>
	<title>Styling guide</title>
</head>
<body style="background: #e71515">
	<h1 style="color: #ffffff">This is a document</h1>
</body>
</html>
```

- Conflict resoultion in web page \
Whenever there are multiple styling arguments in a html document the html always seeks for element level styling in the beginning heading styles as the intermediate amd external styling in the end.
### Adding a hyperlink
A hyperlink is a gateway to another website or can be a local file. A hyperlink can be enclosed withing a string of text, a button or an image. \
In this example we have two files one is index.html and the another is child.html the hyperlink in the file is bidirectional. \
- Contents of index.html
```html
<!DOCTYPE html>
<html lang="en">
<head>
	<title>First webpage</title>
</head>
<body>
	<h1>Hello world</h1>
	<p> <b>This </b>is <i>a </i>simply simply <u>lovleh </u>paragraph</p>
	<a href = "child1.html">Child link</a>
</body>
</html>
```
- Contents of child.html
```html
<!DOCTYPE html>
<html lang="en">
<head>
	<title>Child</title>
</head>
<body>
	<h1>This is the child app</h1>
	<!-- this is a standard hyprlink -->
	<!-- this is an relative url -->
	<a href="index.html">Click on this</a>
</body>
</html>
```
There are two types of urls. Absolute urls and relative urls. Absolute urls give the complete location of the file but may change from system to system but using relative urls promises that the program will work on any system with the same OS. \
This is an example of an external hyperlink where the link navigates to anoter file or webpage.

- By using internal hyperlink
```html
<!DOCTYPE html>
<html lang="en">
<head>
	<title>First webpage</title>
</head>
<body>
	<div id = "Top"></div>
	<a href="index.html#Bottom">Bottom</a>
	<h1>Lewis Hamilton</h1>
	<p>Sir Lewis Carl Davidson Hamilton MBE HonFREng (born 7 January 1985) is a British racing driver currently competing in Formula One for Mercedes. In Formula One, Hamilton has won a joint-record seven World Drivers' Championship titles (tied with Michael Schumacher), and holds the records for the most wins (103), pole positions (103), and podium finishes (191), among others.
	<div id="Bottom"></div>
	<h1>Max Verstappen</h1>
	<p>A speedy boi</p>
	<a href = "index.html#Top">Top</a>
</body>
</html>
```
image maps
background color, entire page, particular page, rgb and hex colors, alpha colors in html

## Styling

### Comments
CSS supports c style block comments
```css
/* this is a comment */
```
### Background color
Background color can be added in html webpage by two ways, first directly using the html format and adding colour int the html document. The second way is to use a CSS document to stylize individual element.

- Simple method
```html
<!DOCTYPE html>
<html>
<!-- opacity also set -->
<body style="background-color:powderblue; opacity: 30%">

<h1>This is a heading</h1>
<p>This is a paragraph.</p>

</body>
</html>
```
- Using CSS \
Contents of HTML document
```html
<!DOCTYPE html>
<html>
<head>
	<link rel="stylesheet" href="style.css">
</head>
<body>

<h1>This is a heading</h1>
<p>This is a paragraph.</p>

</body>
</html>
```
Contents of CSS document
```css
body {background-color: powderblue;}
```

### The div tag
The div tag cann be used in html and css to define the space in between.
```html
<!DOCTYPE html>
<html>
<style>
	h1 {
	background-color: orange;
	}

	div {
	background-color: blue;
	}

	p {
	background-color: green;
	}
</style>
<body>
	
<div>
<h1>This is a heading</h1>
<p>This is a paragraph.</p>
</div>
</body>
</html>
```

### Background image

- Adding background image from url
```html
<style>
	body {
		background-image: url("https://img.freepik.com/free-vector/blue-pink-halftone-background_53876-99004.jpg?w=2000");
	}
</style>
```

Other background tags can be found [here](https://www.w3schools.com/css/css_background.asp)

### Border
Border can be formed with these attributes
```html
<!DOCTYPE html>
<html>
<style>
	p.mix {
		/* Change of border style and thickness */
		border-style: dotted dashed double;
		border-width: thick;
	}
</style>
<body>
	
<div>
<h1>This is a heading</h1><br>
<p class="mix">This is a paragraph.</p>
</div>
</body>
</html>
```
Other border attributes can be found [here](https://www.w3schools.com/css/css_border.asp) \
Border always happens from **top right bottom left**. \
Shorthand notation can be used in the following way.
```html
<!DOCTYPE html>
<html>
<style>
	p.mix {
		/* shorthand notation in action */
		border: solid blue 10px;
	}
</style>
<body>
	
<div>
<h1>This is a heading</h1><br>
<p class="mix">This is a paragraph.</p>
</div>
</body>
</html>
```
### Customising the font
The font can be customised in a lot of ways in html, that is the user can change the size, the weight and the type of font used

- Using HTML \
```html
<!DOCTYPE html>
<html>
<head>
	<!-- <link rel="stylesheet" href="style.css"> -->
</head>
<body>

	
	<h1 "font-family:verdana;" style="font-size:300%;">This is a heading</h1>
	<p>This is a paragraph.</p>

</body>
</html>
```
- Using CSS \
Contents of html document
```html
<!DOCTYPE html>
<html>
<head>
	<link rel="stylesheet" href="style.css">
</head>
<body>

<h1>This is a heading</h1>
<p>This is a paragraph.</p>

</body>
</html>
```
Contents of CSS file
```css
body {
	/* Changing the background color */
	background-color: rgb(255, 255, 255);
}
/* here h1 is the p type element selector*/
h1 {
	/* Changing the font size */
	font-size: 5em;
	/* Changing the font style */
	font-style: oblique;
	/* Changing the font family */
	font-family: 'Courier New', Courier, monospace;
	/* Changing the font weight */
	font-weight: normal;
	/* Aligning text to center */
	text-align: center;
}
```
A great practice in classifying the font type is to have multiple fonts. This makes sure that if any OS doesn't support the font that is asked to be rendered another placeholer font will replace it so the styling of the website is not inconsistant.

### Styling basics 
- Box model \
The whole webpage is divided into padding, border and margin with the margin being the differentialtor between the current element and the end of the current element. The Border being the end of the space between padding and margin and the padding is the void between the content and the border.

### Styling individual elements
With muliple elements requiring different styles, we can use html with css to assign certain id with certain elements to having individual styles.

- Using ID selector
```html
<!DOCTYPE html>
<html lang="en">
<head>
	<title>Styling guide</title>
</head>
<style>
	body {
	background: #ffffff;
	}
	h1 {
		color: #000000;
	}
	#color {
		color: crimson;
	}
</style>
<body>
	<h1>This is a document</h1>
	<p>This is the not coloured paragraph style.</p>
	<br><br>
	<p id="color">This is a colouted paragraph</p>
</body>
</html>
```

- Using class selector
```html
<!DOCTYPE html>
<html lang="en">
<head>
	<title>Styling guide</title>
</head>
<style>
	body {
		background: #ffffff;
	}
	h1 {
		color: #000000;
	}
	.color {
		color: crimson;
	}
</style>
<body>
	<h1>This is a document</h1>
	<p>This is the not coloured paragraph style.</p>
	<br><br>
	<p class="color">This is a colouted paragraph</p>
</body>
</html>
```

### Generic and non generic selectors in CSS
Generic selectors in CSS are the normal selectors used in above programs and change all the elements with the given tag, whereas non generic selectors only change the type of file which matches the given id attribute and the type of tag it has.

```html
<!DOCTYPE html>
<html lang="en">
<head>
	<title>Styling guide</title>
</head>
<style>
	body {
	background: #ffffff;
	}
	h1 {
		color: #000000;
	}
	/* non generic styles used here */
	p.color {
		color: crimson;
	}
</style>
<body>
	<h1 class="color">This is a document</h1>
	<p>This is the not coloured paragraph style.</p>
	<br><br>
	<p class="color">This is a colouted paragraph</p>
</body>
</html>
```

### Z index
The Z index is used to create layers in a html form. It being similar to the layer function in photoshop, with -1 being the index that is bedind all the other layers and the positive layers neing in the front of all the other layers.
### Extras
1. Where and where to use class and ID in HTML? ID support dynamic attributes that is powered
2. Class/ID names support spaces but no number in the beginning
3. Universal selector * can be used to highlight all content
4. Grouping selection can be initiated with the tag name and a comma in between.

## Creating a table
There are three keywords in creating a table\
1. table - keyword for initiating a table
2. tr - creates a table row
3. th - creates a table heading
4. td - inserts new table data

Syntax of creating a table
```html
<!DOCTYPE html>
<html>
<head>
	<!-- <link rel="stylesheet" href="style.css"> -->
</head>
<body>
	<!-- Initiating the table -->
	<table>
		<!-- Creates a table row -->
		<tr>
			<!-- Creates a table heading -->
			<th>Srno</th>
			<th>Name</th>
			<th>Qty</th>
		</tr>
		<tr>
			<!-- Inserta table data -->
			<td>1. </td>
			<td>Bruh</td>
			<td>69</td>
		</tr>
	</table>
</body>
</html>
```
Attributes can be modified within a table either using the prebuilt functions in HTML or in CSS.
- In HTML
```html
...
<body>
	<table width="100%" cellspacing = "10" cellpadding = "10">
		<tr>
...
```

Other properties of tables can be changed with style attributes under the table tag. Some operations can be found [here](https://www.w3schools.com/html/html_table_sizes.asp).

## Images
Images can be created inside html with the img tag, the image can either be hosted locally or globally depending on the requirements. The syntax of inserting an image is as follows.

```html
<!DOCTYPE html>
<html lang="en">

<head>
	<title>Document</title>
</head>

<body>
	<h1>Sussy baka</h1>
	<!-- Image 1 inserted -->
	<img src="tmp.jpg" alt="Sus">
	<h1>Waltuh</h1>
	<!-- Image 2 inserted -->
	<img src="waltuh.jpeg" alt="Waltuh">
</body>

</html>
```
Folder contents
1. index.html
2. tmp.jpg
3. waltuh.jpeg

## Forms in HTML
Forms can be used to recieve data from the user and into the erver to perform various operations on the web, they can be used with the following syntax

### Text input
A text field can be used to gather alphanumeric input from the user
```html
<!DOCTYPE html>
<html>
<body>

<h2>HTML Forms</h2>

<form action="/action_page.php">
	<label for="name">Enter name:</label><br>
	<input type="text" id="name" name="roll" value="gp"><br>
	<label for="roll">Last name:</label><br>
	<input type="text" id="roll" name="roll" value="33"><br><br>
	<input type="reset" value="Reset"><br>
	<input type="submit" value="Submit">
</form> 

<p>If you click the "Submit" button, the page willl break</p>

</body>
</html>
```

- Multiline text input
```html
<!DOCTYPE html>
<html>
<body>

<h2>Multiple</h2>
<p>Enter the adress</p>

<form action="child1.html">
	<textarea name="message" rows="10" cols="30">The Ghar</textarea>
	<br><br>
	<input type="submit">
</form>

</body>
</html>
```
### Radio buttons
A radio button only has a fixed input and the user can only select one input at once
```html
<!DOCTYPE html>
<html>
<body>
<h2>Radio Buttons</h2>
<p>Is esteban ocon an asshole?</p>
<form>
	<input type="radio" id="yes" name="ocon" value="yes">
	<label for="yes">Yes</label><br>
	<input type="radio" id="no" name="ocon" value="no">
	<label for="no">No</label><br>
</form> 
</body>
</html>
```
Note that the names of the option should be same otherwise it becomes a multi way selection rather than a single way selection.

### Checkboxes
A checkbox option is similar to the radio button but has the option of choosing multipe options
```html
<!DOCTYPE html>
<html>
<body>

	<h2>Sunday</h2>
	<p>The <strong>input type="checkbox"</strong> defines a checkbox:</p>

	<form action="/file.php">
		<!-- useage of target attribute -->
		<input type="checkbox" id="pole" name="v1" value="Pole" target="parent">
		<label for="pole"><a href="https://www.f1.com/">Pole position</a></label><br>
		<input type="checkbox" id="win" name="v2" value="Win">
		<label for="win"><a href="https://www.f1.com/">Race win</a></label><br>
		<input type="checkbox" id="flap" name="v3" value="Fastest Lap">
		<label for="flap"><a href="https://www.f1.com/">Fastest lap</a></label><br><br>
		<input type="submit" value="Submit">
	</form> 

</body>
</html>
```
Other methods can be checked [here](https://www.w3schools.com/html/html_forms.asp)

- Note: The target tag can be specified to show how the file should be opened, if the target is specified in as the parent window then the hyperlink, or the submit window will open in the same window, if the target is not specified then it will opem in a new tag.

The following tags can be used at the end of the tag to perform certaing applicaitons
1. Autocomplete tag: autocomplete="on"
2. Novalidate: novalidate
The get and the set method can be found [here](https://www.w3schools.com/html/html_forms_attributes.asp)

### Dropdown list
The dropdown list is similar to the radio in the sense that the user can select only one of the options
```html
<!DOCTYPE html>
<html>
<body>
	<h2>Choose a car</h2>
	<label for="cars">Select one</label>
	<!-- Size and multiple being used -->
	<select id="cars" name="cars" size="3" multiple>
	  <option value="mer">Mercedes</option>
	  <!-- Ferrari being the default option -->
	  <option value="fer">Ferrari</option>
	  <option value="rbr">Red Bull</option>
	  <option value="alp">Alpine</option>
	  <option value="mcl">McLaren</option>
	  <option value="amr">Aston Martin</option>
	  <option value="haa">Haas</option>
	  <option value="alt">Alpha Tauri</option>
	  <option value="alr">Alfa Romeo</option>
	  <option value="wil">Williams</option>

	</select>

</body>
</html>
```
1. Size gives the program a more broader width
2. Multiple allows the user to select multiple options with a ctrl+click action

### Buttons
Buttons make the website dynamic with the use of javascript libraries
```html
<!DOCTYPE html>
<html>
<body>

<h2>The button Element</h2>

<button type="button" onclick="alert('Hello World!')">Click Me!</button>

</body>
</html>
```

## Javascript
Javascript is a scripting language rather than a conventional programming language. The program is also object based insted of object oriented programming, so creation of objects can be implemented however not necessary. It also features dynamic variables that means a variable can compute itself, similar to many other common languages `var1 = var1 + 1`.

### Implementing Javascript in the code
Implementation of javascript is very similar to implementation of CSS in a HTML webpage. There are 3 methods of implementing of the javascript code
1. inline - the script is embedded in the html code
2. internal - the script comes before any html file
3. external - a dedicated javascript file is made

### Dynamic html code via JavaScript
The innerhtml code can be used to gater or modify html code, the innerhtml code works with an html tag with a certain allocated `id` and when the id matches the property of that tag can be changed with the innerhtml tag.

### Extras
1. Integer parseint - Changes the datatype of the given string to the first given integer

### A simple Javascript code
```html
<!DOCTYPE html>
<html>
<body>
<script>
	function showdate(){
		document.getElementById('demo').innerHTML = Date();
	}
</script>
<h2>My First JavaScript</h2>

<button type="button" onclick="showdate()">Click me</button>

<p id="demo"></p>

</body>
</html> 
```

### Javascript calculator
```html
<!DOCTYPE html>
<html lang="en">
<head>
	<meta charset="UTF-8">
	<meta http-equiv="X-UA-Compatible" content="IE=edge">
	<meta name="viewport" content="width=device-width, initial-scale=1.0">
	<title>Document</title>
	<script>
		var num1 = prompt('Enter first number: '); num1=num1-0;
		var num2 = prompt('Enter second number: '); num2=num2-0;
		function add() {
			document.getElementById('ans').innerHTML = num1+num2;
		}
		function sub() {
			document.getElementById('ans').innerHTML = num1-num2;
		}
		function mul() {
			document.getElementById('ans').innerHTML = num1*num2;
		}
		function div() {
			document.getElementById('ans').innerHTML = num1/num2;
		}
		function clear() {
			document.getElementById('ans').innerHTML = 'ans';
		}
	</script>
</head>
<body>
	<!-- <form>
		<input type="text" id="theNum1"/>
		<input type="text" id="theNum2"/>
	</form> -->
	<button type="button" onclick="add()">Add numbers</button>
	<button type="button" onclick="sub()">Subtract numbers</button>
	<button type="button" onclick="mul()">Multiply numbers</button>
	<button type="button" onclick="div()">Divide numbers</button>
	<button type="button" onclick="clear()">Clear numbers</button>
	<p id="ans">ans</p>
</body>
</html>
```

Taking user inputs
```html
<!DOCTYPE html>
<html lang="en">
<head>
	<meta charset="UTF-8">
	<meta http-equiv="X-UA-Compatible" content="IE=edge">
	<meta name="viewport" content="width=device-width, initial-scale=1.0">
	<title>Document</title>
	<script>
		var num1, num2;
		function resolve() {
			num1 = document.getElementById('theNum1').value;
			num2 = document.getElementById('theNum2').value;
			num1=num1-0;
			num2=num2-0;
		}
		function add() {
			resolve();
			document.getElementById('ans').innerHTML = num1+num2;
		}
		function sub() {
			resolve();
			document.getElementById('ans').innerHTML = num1-num2;
		}
		function mul() {
			resolve();
			document.getElementById('ans').innerHTML = num1*num2;
		}
		function div() {
			resolve();
			document.getElementById('ans').innerHTML = num1/num2;
		}
		function clear() {
			document.getElementById('ans').innerHTML = 'ans';
		}
	</script>
</head>
<body>
	<form>
		<input type="text" id="theNum1"/>
		<input type="text" id="theNum2"/>
	</form>
	<button type="button" onclick="add()">Add numbers</button>
	<button type="button" onclick="sub()">Subtract numbers</button>
	<button type="button" onclick="mul()">Multiply numbers</button>
	<button type="button" onclick="div()">Divide numbers</button>
	<button type="button" onclick="clear()">Clear numbers</button>
	<p id="ans">ans</p>
</body>
</html>
```

### API'S
API stands for Application Programming Interface. It acts as a bridge between the backend applocation and the frontend web application.

There are two types of API's
1. Browser API - A browser acts as an extension to the browsers current functionality
2. Server API - A server API does the same for the server

Some popular API's 
1. Geolocation API - Gives the precise location of the user
2. Validation API - Validates the input given by the user

Third party API's
Third party API's are the API's built by other users and not the browser, these API's typically need an API key to ensure the use of proper accounts and proper services.

- Web history API
1. Back - May navigate to any page predessing it
2. Forward - May navigate to any page sucessiding it
3. Go - Will navigate to any given page in the history

javascript fetch api

## Using a web server
A web server can used to execute fetch api protocols, XAMPP, WAMPP can be used if you are on windows or Apache can be used if you are on linux and all the other requirements are also installed.

- Installing Apache as a web server on linux \
Open your linux terminal and execute the following commands
1. Updating the system
```bash
sudo apt update
sudo apt upgrade
```
2. Installing php
```bash
sudo apt install php
```
3. Installing apache
```bash
sudo apt install apache2
```
4. Installing mariadb
```bash
# getting the client
sudo apt install mariadb-server mariadb-client -y

# checking the gpg keys
sudo apt-key adv --fetch-keys 'https://mariadb.org/mariadb_release_signing_key.asc'

# adding the gpg keys
sudo add-apt-repository 'deb [arch=amd64,arm64,ppc64el] https://mariadb.mirror.liquidtelecom.com/repo/10.6/ubuntu focal main'

# installign the client
sudo apt update && sudo apt install -y mariadb-server mariadb-client
```
If mariadb is installed then it can be checked by
```bash
mariadb --version
```
Enabling mariadb
```bash
sudo systemctl start mariadb
sudo systemctl enable mariadb
```
Configuring mariadb
```bash
sudo mysql_secure_installation
```
Adding a password \
Replace _enter_your_password_ by your own custom password
```bash
sudo mariadb -u root -p
CREATE USER 'admin_user'@'localhost' IDENTIFIED BY 'enter_your_password';
```

- Acessing Apache \
Enter this on the terminal \
Starting the server
```bash
sudo service apache2 start
```
File location \
All the files in apache are stored in this specific location if you want to add or change the webpage you can go to the following location
```bash
cd /var/www/html
```

- Opening the server \
Enter this in the terminal
```bash
hostname -i
```
Now copy the ip and repace it in _enter_the_ip_
```
http://enter_the_ip
```

note: hostgator to host servers

## Styling using external libraries

### Bootstrap
Bootstrap is a external css library which can be used to stylze the html webpage. It also allows the user to make responsive pages in order for the app to work across multiple devices with different aspect ratios and different screen sizes.

- Versions of bootstrap \
Currently bootstrap 3 is considered as legacy but is also the most stable and bootstrap 5 is the most recent with bootstrap 4 being the awkard middle child. The previous versions have been depricated.

- Container \
A container is a housing of different in the html file using bootstrap. There are two kinds of containters
1. Container (standard): A housing of diffeent elements that occupies fixed space
2. Fluid container: A housing of different elements that occupies the full screen

```html
<!DOCTYPE html>
<html lang="en">
<head>
  <title>Bootstrap Example</title>
  <meta charset="utf-8">
  <meta name="viewport" content="width=device-width, initial-scale=1">
  <link href="https://cdn.jsdelivr.net/npm/bootstrap@5.2.3/dist/css/bootstrap.min.css" rel="stylesheet">
  <script src="https://cdn.jsdelivr.net/npm/bootstrap@5.2.3/dist/js/bootstrap.bundle.min.js"></script>
</head>
<body>
  
<div class="container">
  <h1>My First Bootstrap Page</h1>
  <p>This part is inside a .container class.</p>
  <p>The .container class provides a responsive fixed width container.</p>
  <p>Resize the browser window to see that the container width will change at different breakpoints.</p>
</div>

</body>
</html>
```
**Note** that the link to other web pages can also be stored locally and can be linked like just any others web pages.

- Padding \
The padding can be changes with the `p` tag. For example here we are changing the top pading by 5 units
```html
<div class="container pt-5"></div>
```
Note that this should be used in conjunction to the previous code with the containter line to be tweaked. \
The `pt` stands for _padding-top_ it can be changed `pb`, `pl`, `pr` to change other attributes. \
Similarly the `m` keyword stands for margins, and can be used as a compound attribute.

Example on padding and margins
```html
<!DOCTYPE html>
<html lang="en">
<head>
  <title>Bootstrap Example</title>
  <meta charset="utf-8">
  <meta name="viewport" content="width=device-width, initial-scale=1">
  <link href="https://cdn.jsdelivr.net/npm/bootstrap@5.2.3/dist/css/bootstrap.min.css" rel="stylesheet">
  <script src="https://cdn.jsdelivr.net/npm/bootstrap@5.2.3/dist/js/bootstrap.bundle.min.js"></script>
</head>
<body>
  
<div class="container p-5 my-5 border">
  <h1>My First Bootstrap Page</h1>
  <p>This container has a border and some extra padding and margins.</p>
</div>

<div class="container p-5 my-5 bg-black text-white">
  <h1>My First Bootstrap Page</h1>
  <p>This container has a dark background color and a white text, and some extra padding and margins.</p>
</div>

<div class="container p-5 my-5 bg-primary text-white">
  <h1>My First Bootstrap Page</h1>
  <p>This container has a blue background color and a white text, and some extra padding and margins.</p>
</div>

</body>
</html>
```

- Containter sizes
The `.container-sm|md|lg|xl` classes to determine when the container should be responsive.
The max-width of the container will change on different screen sizes/viewports and can be adapted to any screen.
```html
<!DOCTYPE html>
<html lang="en">
<head>
  <title>Bootstrap Example</title>
  <meta charset="utf-8">
  <meta name="viewport" content="width=device-width, initial-scale=1">
  <link href="https://cdn.jsdelivr.net/npm/bootstrap@5.2.3/dist/css/bootstrap.min.css" rel="stylesheet">
  <script src="https://cdn.jsdelivr.net/npm/bootstrap@5.2.3/dist/js/bootstrap.bundle.min.js"></script>
</head>
<body>
  
<div class="container pt-3">
  <h1>Responsive Containers</h1>
  <p>Resize the browser window to see the effect.</p>
</div>

<div class="container-sm border">.container-sm</div>
<div class="container-md mt-3 border">.container-md</div>
<div class="container-lg mt-3 border">.container-lg</div>
<div class="container-xl mt-3 border">.container-xl</div>
<div class="container-xxl mt-3 border">.container-xxl</div>

</body>
</html>
```

- Responsive columns
Tables are responsive but are unable to reform when the aspect ratio i changed. With bootstrap and responsive colums the columns automatically reform when the device width is changed.
```html
<!DOCTYPE html>
<html lang="en">
<head>
  <title>Bootstrap Example</title>
  <meta charset="utf-8">
  <meta name="viewport" content="width=device-width, initial-scale=1">
  <link href="https://cdn.jsdelivr.net/npm/bootstrap@5.2.3/dist/css/bootstrap.min.css" rel="stylesheet">
  <script src="https://cdn.jsdelivr.net/npm/bootstrap@5.2.3/dist/js/bootstrap.bundle.min.js"></script>
</head>
<body>
  
<div class="container-fluid mt-3">
  <h1>Responsive Columns</h1>
  <p>Resize the browser window to see the effect.</p>
  <p>The columns will automatically stack on top of each other when the screen is less than 576px wide.</p>
  <div class="row">
    <div class="col-sm-3 p-3 bg-primary text-white">.col</div>
    <div class="col-sm-3 p-3 bg-dark text-white">.col</div>
    <div class="col-sm-3 p-3 bg-primary text-white">.col</div>
    <div class="col-sm-3 p-3 bg-dark text-white">.col</div>
  </div>
</div>

</body>
</html>
```

- Displaying stuff in bootstrap
```html
<!DOCTYPE html>
<html lang="en">
<head>
  <title>Bootstrap Example</title>
  <meta charset="utf-8">
  <meta name="viewport" content="width=device-width, initial-scale=1">
  <link href="https://cdn.jsdelivr.net/npm/bootstrap@5.2.3/dist/css/bootstrap.min.css" rel="stylesheet">
  <script src="https://cdn.jsdelivr.net/npm/bootstrap@5.2.3/dist/js/bootstrap.bundle.min.js"></script>
</head>
<body>

<div class="container mt-3">
  <p>The font-size of each Bootstrap heading depends on the screen size. Try to resize the browser window to see the effect.</p>
  <h1 class="display-1 >h1 Bootstrap heading</h1>
  <h2 class="display-2 >h2 Bootstrap heading</h2>
  <h3 class="display-3 >h3 Bootstrap heading</h3>
  <h4 class="display-4 >h4 Bootstrap heading</h4>
  <h5 class="display-5 >h5 Bootstrap heading</h5>
  <h6 class="display-6 >h6 Bootstrap heading</h6>
</div>

</body>
</html>
```

This can be changed to smaller font like this
```html
 <h1>h1 heading <small>secondary text</small></h1>
 <h2>h2 heading <small>secondary text</small></h2>
 <h3>h3 heading <small>secondary text</small></h3>
 <h4>h4 heading <small>secondary text</small></h4>
 <h5>h5 heading <small>secondary text</small></h5>
 <h6>h6 heading <small>secondary text</small></h6>
```

- Text colours \
Bootstrap has its own colours to specify \
These are
1. .text-muted
2. .text-primary
3. .text-success
4. .text-info
5. .text-warning
6. .text-danger
7. .text-secondary
8. .text-white
9. .text-dark
10. .text-body
11. .text-light:
```html
<!DOCTYPE html>
<html lang="en">
<head>
  <title>Bootstrap Example</title>
  <meta charset="utf-8">
  <meta name="viewport" content="width=device-width, initial-scale=1">
  <link href="https://cdn.jsdelivr.net/npm/bootstrap@5.2.3/dist/css/bootstrap.min.css" rel="stylesheet">
  <script src="https://cdn.jsdelivr.net/npm/bootstrap@5.2.3/dist/js/bootstrap.bundle.min.js"></script>
</head>
<body>

<div class="container mt-3">
  <h2>Contextual Colors</h2>
  <p>Use the contextual classes to provide "meaning through colors":</p>
  <p class="text-muted">This text is muted.</p>
  <p class="text-primary">This text is important.</p>
  <p class="text-success">This text indicates success.</p>
  <p class="text-info">This text represents some information.</p>
  <p class="text-warning">This text represents a warning.</p>
  <p class="text-danger">This text represents danger.</p>
  <p class="text-secondary">Secondary text.</p>
  <p class="text-dark">This text is dark grey.</p>
  <p class="text-body">Default body color (often black).</p>
  <p class="text-light">This text is light grey (on white background).</p>
  <p class="text-white">This text is white (on white background).</p>
</div>

</body>
</html>
```

- Using contrasting colors \
Contrasting colors make the webpage be easy to read and is builtin inside bootstrap.
```html
<!DOCTYPE html>
<html lang="en">
<head>
  <title>Bootstrap Example</title>
  <meta charset="utf-8">
  <meta name="viewport" content="width=device-width, initial-scale=1">
  <link href="https://cdn.jsdelivr.net/npm/bootstrap@5.2.3/dist/css/bootstrap.min.css" rel="stylesheet">
  <script src="https://cdn.jsdelivr.net/npm/bootstrap@5.2.3/dist/js/bootstrap.bundle.min.js"></script>
</head>
<body>

<div class="container mt-3">
  <h2>Background Color with Contrasting Text Color</h2>
  <p class="text-bg-primary">This text is important.</p>
  <p class="text-bg-success">This text indicates success.</p>
  <p class="text-bg-info">This text represents some information.</p>
  <p class="text-bg-warning">This text represents a warning.</p>
  <p class="text-bg-danger">This text represents danger.</p>
  <p class="text-bg-secondary">Secondary background color.</p>
  <p class="text-bg-dark">Dark grey background color.</p>
  <p class="text-bg-light">Light grey background color.</p>
</div>

</body>
</html>
```

- Example of striped tables in bootstrap

```html
<!DOCTYPE html>
<html lang="en">
<head>
  <title>Bootstrap Example</title>
  <meta charset="utf-8">
  <meta name="viewport" content="width=device-width, initial-scale=1">
  <link href="https://cdn.jsdelivr.net/npm/bootstrap@5.2.3/dist/css/bootstrap.min.css" rel="stylesheet">
  <script src="https://cdn.jsdelivr.net/npm/bootstrap@5.2.3/dist/js/bootstrap.bundle.min.js"></script>
</head>
<body>

<div class="container mt-3">
  <h2>Striped Rows</h2>
  <p>The .table-striped class adds zebra-stripes to a table:</p>            
  <table class="table table-striped">
    <thead>
      <tr>
        <th>Firstname</th>
        <th>Lastname</th>
        <th>Email</th>
      </tr>
    </thead>
    <tbody>
      <tr>
        <td>John</td>
        <td>Doe</td>
        <td>john@example.com</td>
      </tr>
      <tr>
        <td>Mary</td>
        <td>Moe</td>
        <td>mary@example.com</td>
      </tr>
      <tr>
        <td>July</td>
        <td>Dooley</td>
        <td>july@example.com</td>
      </tr>
    </tbody>
  </table>
</div>

</body>
</html>
```

- Paginations \
Paginations are splitting a page into multiple areas. 
```html
<!DOCTYPE html>
<html lang="en">
<head>
  <title>Bootstrap Example</title>
  <meta charset="utf-8">
  <meta name="viewport" content="width=device-width, initial-scale=1">
  <link href="https://cdn.jsdelivr.net/npm/bootstrap@5.2.3/dist/css/bootstrap.min.css" rel="stylesheet">
  <script src="https://cdn.jsdelivr.net/npm/bootstrap@5.2.3/dist/js/bootstrap.bundle.min.js"></script>
</head>
<body>

<div class="container mt-3">
  <h2>Pagination</h2>
  <p>To create a basic pagination, add the .pagination class to an ul element. Then add the .page-item to each li element and a .page-link class to each link inside li:</p>                  
  <ul class="pagination">
    <li class="page-item"><a class="page-link" href="#">Previous</a></li>
    <li class="page-item"><a class="page-link" href="#">1</a></li>
    <li class="page-item"><a class="page-link" href="#">2</a></li>
    <li class="page-item"><a class="page-link" href="#">3</a></li>
    <li class="page-item"><a class="page-link" href="#">Next</a></li>
  </ul>
</div>

</body>
</html>
```

htmx - extra

tailwind css
```html
<!doctype html>
<html>
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <script src="https://cdn.tailwindcss.com"></script>
</head>
<body>
  <h1 class="text-3xl font-bold underline">
    Hello world!
  </h1>
</body>
</html>
```