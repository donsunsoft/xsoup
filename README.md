Xsoup
----
[![Build Status](https://api.travis-ci.org/code4craft/xsoup.png?branch=master)](https://travis-ci.org/code4craft/xsoup)

XPath selector based on Jsoup.

## Get started:

```java
    @Test
    public void testSelect() {
        String html = "<html><div><a href='https://github.com'>github.com</a></div></html>";

        Document document = Jsoup.parse(html);

        String result = Xsoup.select(document, "//a/@href").get();
        Assert.assertEquals("https://github.com", result);

        result = Xsoup.compile("//a/@href").evaluate(document).get();
        Assert.assertEquals("https://github.com", result);
    }
```

## Performance:

Xsoup use Jsoup as HTML parser. 

Compare with another most used XPath selector for HTML - [**`HtmlCleaner`**](http://htmlcleaner.sourceforge.net/), Xsoup is much faster:

	Normal HTML, size 44KB
	XPath: "//a"	| 	CSS Selector: "a"
	Run for 2000 times

	Environment：Mac Air MD231CH/A 
	CPU: 1.8Ghz Intel Core i5

<table>
    <tr>
        <td width="100">Operation</td>
        <td width="100">Xsoup</td>
        <td>HtmlCleaner</td>
    </tr>
    <tr>
        <td>parse</td>
        <td>3,207(ms)</td>
        <td>7,999(ms)</td>
    </tr>
    <tr>
        <td>select</td>
        <td>95(ms)</td>
        <td>380(ms)</td>
    </tr>
</table>

## Syntax supported:

### XPath1.0:

<table>
    <tr>
        <td width="100">Name</td>
        <td width="100">Expression</td>
        <td>Support</td>
    </tr>
    <tr>
        <td>nodename</td>
        <td>nodename</td>
        <td>yes</td>
    </tr>
    <tr>
        <td>immediate parent</td>
        <td>/</td>
        <td>yes</td>
    </tr>
    <tr>
        <td>parent</td>
        <td>//</td>
        <td>yes</td>
    </tr>
    <tr>
        <td>attribute</td>
        <td>[@key=value]</td>
        <td>yes</td>
    </tr>
    <tr>
        <td>nth child</td>
        <td>tag[n]</td>
        <td>yes</td>
    </tr>
    <tr>
        <td>attribute</td>
        <td>/@key</td>
        <td>yes</td>
    </tr>
    <tr>
        <td>wildcard in tagname</td>
        <td>/*</td>
        <td>yes</td>
    </tr>
    <tr>
        <td>function</td>
        <td>function()</td>
        <td>part</td>
    </tr>
    <tr>
        <td>or</td>
        <td>a | b</td>
        <td>no</td>
    </tr>
    <tr>
        <td>parent in path</td>
        <td>. or ..</td>
        <td>no</td>
    </tr>
    <tr>
        <td>predicates</td>
        <td>price>35</td>
        <td>no</td>
    </tr>
</table>

### Function supported:

<table>
    <tr>
        <td width="100">Expression</td>
        <td width="100">Description</td>
        <td>Support</td>
    </tr>
    <tr>
        <td width="100">text()</td>
        <td width="100">text content of element</td>
        <td>yes</td>
    </tr>
    <tr>
        <td width="100">regex(expr)</td>
        <td width="100">use regex to extract content</td>
        <td>todo</td>
    </tr>
</table>