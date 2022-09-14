<h1>The URL Regex - A Tutorial</h2>

Hi, there! Welcome to my Regex Tutorial gist! In this gist, I'll be dissecting a regular expression that can be used to verify a URL matches given parameters.

<h2 style='text-align: center;'>Summary</h2>

<div style='text-align: center;'>

**The Regex**  

`/^(https?:\/\/)?([\da-z\.-]+)\.([a-z\.]{2,6})([\/\w \.-]*)*\/?$/`

The regular expression above can be used to verify that a URL follows a specific format. In the following sections, I'll break the regex down and explain what each section is doing. 

</div><br />

<h2 style='text-align: center;'>Table of Contents</h2>

- [Regex Components](#regex-components)
  - [Character Classes](#character-classes)
    - [Character Class Examples](#character-class-examples)
  - [Escaped Characters](#escaped-characters)
  - [Anchors](#anchors)
    - [Anchors Examples](#anchors-examples)
  - [Quantifiers](#quantifiers)
    - [Quantifiers Examples](#quantifiers-examples)
  - [Grouping and Capturing](#grouping-and-capturing)
    - [Grouping and Capturing Examples](#grouping-and-capturing-examples)
  - [Bracket Expressions](#bracket-expressions)
    - [Bracket Expressions Examples](#bracket-expressions-examples)
- [Conclusion](#conclusion)
- [Author](#author)

## Regex Components

The basic components of any regex include character classes, anchors, quantifiers, and grouping. 
Character classes are used to include different types of characters in a regex comparison. 
Anchors specify the start or end of a word or line (if the multiline flag is used). 
Grouping creates sections that can be used to allow quantities of the same section in a row, as well as other useful techniques. 

### Character Classes

<div style='font-family: monospace'>
/^(https?:\/\/)?([
<span style='color: #09FFCA; font-weight: bold;'>\da-z</span>
\.-]+)\.([
<span style='color: #09FFCA; font-weight: bold;'>a-z</span>
\.]{2,6})([\/
<span style='color: #09FFCA; font-weight: bold;'>\w</span>
 \.-]*)*\/?$/

</div><br />

In regular expressions, character classes are used to search for types of characters rather than specific ones. 
In the regular expression for URLs, <span style='color: #09FFCA; font-family: monospace; font-weight: bold;'>\d</span> refers to digits from 0 to 9.

To search for characters in a range, <span style='color: #09FFCA; font-family: monospace; font-weight: bold;'>a-z</span> or <span style='color: #09FFCA; font-family: monospace; font-weight: bold;'>0-9</span> will do the trick. 
The <span style='color: #09FFCA; font-family: monospace; font-weight: bold;'>a-z</span> character class in our URL regex is a range character class. 
You can specify a character range by simply changing the starting and ending values, like <span style='color: #09FFCA; font-family: monospace; font-weight: bold;'>c-g</span>. 
It's important to note that letter ranges are case sensitive. 
So <span style='color: #09FFCA; font-family: monospace; font-weight: bold;'>a-z</span> is specific to lowercase letters and <span style='color: #09FFCA; font-family: monospace; font-weight: bold;'>A-Z</span> to uppercase.
  
The last character class in our URL regex, <span style='color: #09FFCA; font-family: monospace; font-weight: bold;'>\w</span>, refers to any word character. 
A word character is any letter, number, or underscore.

#### Character Class Examples

<span style='color: #09FFCA; font-weight: bold; font-family: monospace;'>\\/</span>

---

Would satisfy: 
  - foo
  - 123
  - foo123

Would *not* satisfy:
  - Foo
  - 1_2_3
  - Foo_Bar

<span style='color: #09FFCA; font-weight: bold; font-family: monospace;'>a-z</span>

---

Would satisfy: 
  - foo
  - bar
  - foobar

Would *not* satisfy:
  - Foo
  - 1_2_3
  - Foo_Bar

### Escaped Characters

<div style='font-family: monospace'>
/^(https?:
<span style='color: #093eff; font-weight: bold;'>\/\/</span>
)?([\da-z
<span style='color: #093eff; font-weight: bold;'>\.</span>
-]+)
<span style='color: #093eff; font-weight: bold;'>\.</span>
([a-z
<span style='color: #093eff; font-weight: bold;'>\.</span>
]{2,6})([
<span style='color: #093eff; font-weight: bold;'>\/</span>
\w 
<span style='color: #093eff; font-weight: bold;'>\.</span>
-]*)*
<span style='color: #093eff; font-weight: bold;'>\/</span>
?$/

</div><br />

Some characters for regular expressions are reserved for various operations. 
For example, a '.' is used to search for any character that is not whitespace (carriage return, tab, or space). 
To search for the character specifically, an escape character has to be placed immediately for it. 
  
In our URL regex, we have multiple occurances of two escaped characters: 
<span style='color: #093eff; font-family: monospace; font-weight: bold;'>\\/</span> and <span style='color: #093eff; font-family: monospace; font-weight: bold;'>\\.</span>. 

<span style='color: #093eff; font-family: monospace; font-weight: bold;'>\\/</span> allows us to look for '/' in strings while <span style='color: #093eff; font-family: monospace; font-weight: bold;'>\\.</span> will search for '.', instead.

### Anchors

<div style='font-family: monospace'>
/<span style='color: #84249F; font-weight: bold;'>^</span>
(https?:\/\/)?([\da-z\.-]+)\.([a-z\.]{2,6})([\/\w \.-]*)*\/?
<span style='color: #84249F; font-weight: bold;'>$</span>
/

</div><br />

The purple text above highlights the anchor elements of this regex.  
<span style='color: #84249F; font-family: monospace; font-weight: bold;'>^</span> is used to denote the start of a word (or line if the multiline flag is used).
In this instance, it signifies the start of the URL and requires that nothing can come before the first group in the regex.  

Similarly, <span style='color: #84249F; font-family: monospace; font-weight: bold;'>$</span> denotes the end of a word (or line if the multiline flag is used). 
It signifies the end of the URL and prevents any other element from being included after the end of the regex.

#### Anchors Examples

`/^(https?:\/\/)?([\da-z\.-]+)\.([a-z\.]{2,6})([\/\w \.-]*)*\/?$/`

Since the entire regular expression is wrapped by a starting and ending anchor, only a completely valid URL string will satisfy the requirements.

---

Would satisfy: 
  - http://github.com/
  - https://www.google.com
  - regexr.com
  - www.devbritt.me

Would *not* satisfy:
  - http://localhost:3001/
  - www.git_hub.com
  - .This.Is.Not.A.URL.

### Quantifiers

<div style='font-family: monospace'>
/^(https
<span style='color: #FF093E; font-weight: bold;'>?</span>
:\/\/)
<span style='color: #FF093E; font-weight: bold;'>?</span>
([\da-z\.-]
<span style='color: #FF093E; font-weight: bold;'>+</span>
)\.([a-z\.]
<span style='color: #FF093E; font-weight: bold;'>{2,6}</span>
)([\/\w \.-]
<span style='color: #FF093E; font-weight: bold;'>*</span>
)
<span style='color: #FF093E; font-weight: bold;'>*</span>
\/
<span style='color: #FF093E; font-weight: bold;'>?</span>
$/

</div><br />

To say that an element is optional, place a <span style='color: #FF093E; font-family: monospace; font-weight: bold;'>?</span> immediately following. 
In our URL regex, it allows us to account for 'http' or 'https' as the protocol scheme by making 's' optional. 
The second <span style='color: #FF093E; font-family: monospace; font-weight: bold;'>?</span> comes after a [group](#grouping-and-capturing) and makes the entire protocol scheme optional, as well. 
The final <span style='color: #FF093E; font-family: monospace; font-weight: bold;'>?</span> allows for an optional ending '/'.
  
Using <span style='color: #FF093E; font-family: monospace; font-weight: bold;'>+</span> in a regex means there can be any number of the previous element, but has to match at least 1. 
In the URL regex, we use <span style='color: #FF093E; font-family: monospace; font-weight: bold;'>+</span> to allow any number of the preceeding characters for the URL subdomain and second-level domain.   
  
To allow only a specific quantity of the preceeding element, <span style='color: #FF093E; font-family: monospace; font-weight: bold;'>{x}</span> or <span style='color: #FF093E; font-family: monospace; font-weight: bold;'>{x,y}</span> can be used. 
The quantifier <span style='color: #FF093E; font-family: monospace; font-weight: bold;'>{2,6}</span> in our regex specifies how many characters can make up the top-level domain.  
  
<span style='color: #FF093E; font-family: monospace; font-weight: bold;'>*</span> is like a comibination of <span style='color: #FF093E; font-family: monospace; font-weight: bold;'>?</span> and <span style='color: #FF093E; font-family: monospace; font-weight: bold;'>+</span>. 
Placing it after an element means that element can be included any number of times. 
However, unlike <span style='color: #FF093E; font-family: monospace; font-weight: bold;'>+</span>, it doesn't require at least one appearance of the element. 
For the URL regex, it is used to account for any number of subdirectories.

#### Quantifiers Examples

http<span style='color: #FF093E; font-weight: bold; font-family: monospace;'>s?</span>

---

Would satisfy: 
  - http
  - https

Would *not* satisfy:
  - htp
  - htps
  - www

(https?:\\ /\\ /)<span style='color: #FF093E; font-weight: bold; font-family: monospace;'>?</span>

---

Would satisfy: 
  - http://
  - https://
  - Could also be blank since <span style='color: #FF093E; font-weight: bold; font-family: monospace;'>?</span> makes the entire group optional

Would *not* satisfy:
  - http:
  - https:/
  - /http
  
[\\da-z\\.-]<span style='color: #FF093E; font-weight: bold; font-family: monospace;'>+</span>

---

Would satisfy: 
  - github
  - www.regexr
  - blog.1-2-many

Would *not* satisfy:
  - GitHub
  - www_devBritt
  - blog.1_2_many
  
\\.([a-z\\.]<span style='color: #FF093E; font-weight: bold; font-family: monospace;'>{2,6}</span>)

---

Would satisfy: 
  - .edu
  - .io
  - .com.au

Would *not* satisfy:
  - .EDU
  - .Io
  - .com-au
  
([\\ / \\w \\.-]<span style='color: #FF093E; font-weight: bold; font-family: monospace;'>\*</span>)<span style='color: #FF093E; font-weight: bold; font-family: monospace;'>\*</span>

---

Would satisfy: 
  - /about
  - /api/users
  - /about-us
  - /terms.en

Would *not* satisfy:
  - /About
  - /api=users
  - /about_us

### Grouping and Capturing

<div style='font-family: monospace'>
/^
<span style='color: #FF6A24; font-weight: bold;'>(</span>
https?:\/\/
<span style='color: #FF6A24; font-weight: bold;'>)</span>
?
<span style='color: #FF6A24; font-weight: bold;'>(</span>
[\da-z\.-]+
<span style='color: #FF6A24; font-weight: bold;'>)</span>
\.
<span style='color: #FF6A24; font-weight: bold;'>(</span>
[a-z\.]{2,6}
<span style='color: #FF6A24; font-weight: bold;'>)</span>
<span style='color: #FF6A24; font-weight: bold;'>(</span>
[\/\w \.-]*
<span style='color: #FF6A24; font-weight: bold;'>)</span>
*\/?$/

</div><br />

Grouping in a regex is just what it sounds like. 
Wrapping expressions in '( )' allows us to group characters together which can then have other operations performed on them. 
For example, <span style='color: #FF6A24; font-family: monospace; font-weight: bold;'>([\\/\\w \\.-]\*)\*</span> is a group that searches for a forward slash, any word character, a space, a period, and a hypen, in that order. 
Then an asterisk (*) is applied to the group which looks for any number of occurances of that group, as stated in the [Quantifiers Section](#quantifiers).
  
The groups in our URL regex are as follows: 
  - <span style='color: #FF6A24; font-family: monospace; font-weight: bold;'>(https?:\\/\\/)</span> is the URL protocol scheme
  - <span style='color: #FF6A24; font-family: monospace; font-weight: bold;'>([\\da-z\\.-]+)</span> refers to the subdomain (ex. 'www.') and second-level domain (ex. 'github')
  - <span style='color: #FF6A24; font-family: monospace; font-weight: bold;'>([a-z\\.]{2,6})</span> is the top-level domain (ex. '.com')
  - <span style='color: #FF6A24; font-family: monospace; font-weight: bold;'>([\\/\\w \\.-]*)</span> checks for subdirectories, if any

#### Grouping and Capturing Examples

<span style='color: #FF093E; font-weight: bold; font-family: monospace;'>(</span>https?:\\ /\\ /<span style='color: #FF093E; font-weight: bold; font-family: monospace;'>)</span>

---

Would satisfy: 
  - http://
  - https://

Would *not* satisfy:
  - htp:/
  - https//

<span style='color: #FF093E; font-weight: bold; font-family: monospace;'>(</span>[\\da-z\\ .-]+<span style='color: #FF093E; font-weight: bold; font-family: monospace;'>)</span>

---

Would satisfy: 
  - github.
  - www.regexr
  - my.colorspace
  - dev-britt7

Would *not* satisfy:
  - GitHub.
  - www/regexr
  - my:colorspace
  - dev_britt7

<span style='color: #FF093E; font-weight: bold; font-family: monospace;'>(</span>[a-z\\ .]{2,6}<span style='color: #FF093E; font-weight: bold; font-family: monospace;'>)</span>

---

Would satisfy: 
  - edu
  - io
  - com.au

Would *not* satisfy:
  - EDU
  - Io
  - com-au

<span style='color: #FF093E; font-weight: bold; font-family: monospace;'>(</span>[\\ / \\w \\.-]*<span style='color: #FF093E; font-weight: bold; font-family: monospace;'>)</span>

---

Would satisfy: 
  - about
  - about-us/
  - terms.en

Would *not* satisfy:
  - About
  - api=
  - about_us
  
### Bracket Expressions

<div style='font-family: monospace'>
/^(https?:\/\/)?(
<span style='color: #FFCA09; font-weight: bold;'>[</span>
\da-z\.-
<span style='color: #FFCA09; font-weight: bold;'>]</span>
+)\.(
<span style='color: #FFCA09; font-weight: bold;'>[</span>
a-z\.
<span style='color: #FFCA09; font-weight: bold;'>]</span>
{2,6})(
<span style='color: #FFCA09; font-weight: bold;'>[</span>
\/\w \.-
<span style='color: #FFCA09; font-weight: bold;'>]</span>
*)*\/?$/

</div><br />

You might be wondering what the difference between grouping and bracket expressions is. 
Grouping says "there is a match if *these characters appear in this order*".
Alternatively, bracket expressions are saying "there is a match if *a single character matches any of these characters*".
Simply put, grouping refers to multiple characters in the string being tested while brackets refer to a single character. 
  
To create a bracket expression, simply wrap them in a bracket pair (<span style='color: #FFCA09; font-weight: bold; font-family: monospace'>[]</span>).
  
The bracket expressions in our URL regex are as follows: 
 - <span style='color: #FFCA09; font-weight: bold; font-family: monospace'>[\\da-z\\.-]</span> specifies the character types that are allowed in the subdomain and second-level domain
 - <span style='color: #FFCA09; font-weight: bold; font-family: monospace'>[a-z\\.]</span> specifies the character types that can make up the top-level domain
 - <span style='color: #FFCA09; font-weight: bold; font-family: monospace'>[\\/\\w \\.-]</span> specifies the character types allowed for subdirectores, if any

#### Bracket Expressions Examples

<span style='color: #FFCA09; font-weight: bold; font-family: monospace'>[\\da-z\\.-]</span>+

---

Would satisfy:
  - www.
  - github.com
  - about.devbritt

Would *not* satisfy:
  - www:
  - GitHub.com
  - about_devbritt

<span style='color: #FFCA09; font-weight: bold; font-family: monospace'>[a-z\\.]</span>{2,6}

---

Would satisfy: 
  - edu
  - io
  - com.au

Would *not* satisfy:
  - EDU
  - Io
  - com-au
  - com3

## Conclusion

Regular expressions can be difficult to understand and even more difficult to construct. 
If you were able to follow along with this tutorial, give yourself a pat on the back! 
If you weren't, check out [regexr.com](https://regexr.com/) and copy and paste the [URL Regex](#summary) at the top of this tutorial into the box at the top. 
Regexr will hilight each expression and describe in detail what it does.

## Author

<span style='color: #09FFCA; font-weight: bold; font-family: monospace;'>Brittany Carlton</span> is an up-and-coming full-stack web developer.
She's excited to explore the world of CSS animations and micro-interactions to build fun and engaging web apps.
She has experience with Javascript, NodeJS, ExpressJS, MySQL, MongoDB, Handlebars, and Bootstrap.
Find her work on [GitHub](https://github.com/devBritt).
