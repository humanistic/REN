# [人] - REN - REadable Notation

## Introduction

**REN** is simple yet powerful data storage, exchange and notation format. It's very human friendly and pleasant to read. 
Every value in **REN** has its own type to allow easier describtion of your data. See for yourself.

There are strings:

    "hello world"

And there are words:
	
	hello world

Numbers are also supported in integer and floating point form.

    1
    -1
    3.14
    -2.354e3

Another type will tell you where to get help:

    http://server.com/readme
	
You get the idea.

The basic form of data collection in REN is block. 
	
    [1 "a" e@ma.il and so://on]	
	
You can also add header to data transmission to inform the loader about type of data.
	
	REN[
		name: Ren
		occupation: "Data language"
		purpose: {
			Easily share data between people and machines.
			Keep the rules simple.
			Be useful.
		}
		version: 0.0.1
		created: 5-Apr-2013
		modified: 13:59:01
		started: 5-Apr-2013/13:59+2:00
		expires: never
	]
	
	home: https://github.com/humanistic/REN
	email: info@ren-lang.org
	complete?: no
	comments-start-with: #";"
	primary-delmiters: [#" " #"^-" #"^/"] ; space tab newline
	
	test: (1 + 1)
	starting-file: %readme.txt
	off-the-beaten: 'a/b/c
	axis: /x
	bin-hex-val: #{48656C6C6F20776F726C6421}
	bin-base-64-val: 64#{SGVsbG8gd29ybGQh}
	
	number-of-supporters: 300
	avg-IQ: 147.35
	cost-to-use: $0.00
	happy-users: 98.6%
	
	common-hashtag: #ren
	screen-size: 1920x1080
	favorite-tag: <bold>
	;favorite-color: 92.128.164
	;lives-at: 127.0.0.1	
	
	object! [
		a: 1
		b: "test"
	]
	
	map! [
		"key 1" 1
		"key 2" "test"
	]
	dataypes: [
		word! string! tuple! date! time! url! email! logic! 
		block! char! paren! file! path! refinement! binary!
		integer! decimal! money! percent! issue! pair! tag!
		object! map!
	]
	
See? It's simple.

###Why?

It's much easier on the eyes than XML and JSON and at the same time it's at least as powerful. Broader datatype support is also great property of REN. 

##Syntax

###Whitespaces

Whitespaces are space, tab and newline. They work as delimiters. There's no comma anywhere. You can put as many whitespaces as you want anywhere you want.

    a:
    [      1
    "b"
          c@d.e ]

is same as

    a: [1 "b" c@d.e]

####Why no comma?

The question is, why comma? 

* Space doesn't visually bother as comma.

* Space key is easier to hit than comma.

* Having (white)space as delimiter allows simple creaton of DSLs or dialects.

See this example:

    send someone@somewhere.com "Something"

In languages with poor datatype support this could be interpreted as:

    {"send","someone@somewhere.com","Something" };

However languages with richer datatype support may understand this as for example Remote Procedure Call  (RPC):

   sendEmail("someone@somewhere.com","Something"");

Just use it as you want to. It's simpler way to express itself.

###Comment  

Comments start with `;`

    ; this is comment

###String

There are two types of string. Single line and multi line. Single line string starts and ends with quotes. Multiline string starts with `{` and ends with `}`. String is UTF-8 encoded. Special characters are escaped with `^` (see table below)

    "single line"

    {multi
    line}


<table>
<tr><th>Character</th>
<th>Definition</th>
<tr>
<td>
^"
</td><td>
Inserts a double quote (").
</td>
<tr>
<td>
^}
</td><td>
Inserts a closing brace (}).
</td>
<tr>
<td>
^^
</td><td>
Inserts a  caret (^).
</td>
<tr>
<td>
^/
</td><td>
Starts a new line.
</td>
<tr>
<td>
^(line)
</td><td>
Starts a new line.
</td>
<tr>
<td>
^-
</td><td>
Inserts a tab.
</td>
<tr>
<td>
^(tab)
</td><td>
Inserts a tab.
</td>
<tr>
<td>
^(page)
</td><td>
Starts a new page.
</td>
<tr>
<td>
^(back)
</td><td>
Erases one character to the left of the insertion point.
</td>
<tr>
<td>
^(null)
</td><td>
Inserts a null character.
</td>
<tr>
<td>
^(escape)
</td><td>
Inserts an escape character.
</td>
<tr>
<td>
^(letter)
</td><td valign="top" bgcolor="white">
Inserts control-letter (A-Z).
</td>
<tr>
<td>
^(xxxx)
</td><td>
Inserts an Unicode character by hexidecimal (xxxx) number.
</td></tr></table>



###Word

Word contains alphanumerical characters, numbers and any of following characters:

    ? ! . ' + - * & | = _

Word cannot start with number. Words are used to construct domain specific languages (DSL) or dialects. More on DSL/dialects later.

    word after word

Some syntax is reserved for future but not currently implemeted:
	
	'world        ; key reference with "'"
	hello :world  ; hello and get 'world key value
	hello: world  ; set hello to 'world
    hello: :world ; set hello to 'world key value
	
###Key (set-word)

Key (also set-word) is used to indicate that word should get following value. Format of set-word is word followed by colon.

    a: 1
    name: "Pepa"
    color: #FF00FF

###Boolean (logic)

There are six boolean values. Why not just two? Because `TRUE` and `FALSE` are not enough. Sometimes it's better to use `YES` or `NO` or `ON` and `OFF`.	

	TRUE
	NO
	ON

###None

`NONE` is value that loader should convert to apropriate value in target language, for example `NULL`.
	
	NONE
	
###Integer

64bit integer number

    1
    -23242

###Floating point

Floating point number

    3.14
    1.2e34

###Email

Standard email - see [RFC5322](http://tools.ietf.org/html/rfc5322#section-3.4.1)

    test@example.com


###URI

Standard URI - see [RFC3986](http://tools.ietf.org/html/rfc3986)
    
    http://www.example.com


###Date and time

Date and time as defined in [RFC3339](http://www.ietf.org/rfc/rfc3339.txt)
You can use slash instead of T, so it's more human readable.

    12:45
    14-3-2013
    1-1-2000/13:20
    1937-01-01T12:00:27.87+00:20

###Block

    [ "this" is: block ]

###Object

Object is collection of set-words (keys) and values kept together in block and prefixed with object! word.

###Map

Map is similiar to object but can have strings as keys. 

##Structure

###Header

Header is optional but you are encouraged to use it. Unless you know what you are sending and where, you should add header as it enhances readability. Header can contain name, type, version, date, checksum and other useful informations about following data. Parse can for example just read header and decide if it makes sense to read rest of data (they may require higher version, data are expired etc.). Format of header is REN followed by block of key/value pairs. Header can be empty also.


