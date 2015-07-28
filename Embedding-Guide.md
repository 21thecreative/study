So, you want to embed a code snippet into your website? No worries, it's simple! 

DartPad offers 3 different embedding choices for shared code. You have the option to show:

1. Dart, Console, and Documentation [embed-dart]
![](https://github.com/dart-lang/dart-pad/blob/master/doc/images/embed-dart.png)
2. Dart, Console, and Html Output (with options to modify HTML/CSS) [embed-html]
![](https://github.com/dart-lang/dart-pad/blob/master/doc/images/embed-html.png)
3. Dart and console only [embed-inline]
![](https://github.com/dart-lang/dart-pad/blob/master/doc/images/embed-inline.png)

DartPad pages use query parameters in the URL to retrieve & show certain information.
This means that users can configure how to show their code by quickly changing the URL.

A sample URL would be 
[https://dartpad.dartlang.org/embed-html.html?id=72d83fe97bfc8e735607&verticalRatio=80](https://dartpad.dartlang.org/embed-html.html?id=72d83fe97bfc8e735607&verticalRatio=80)

It can be embedded by inserting the following code into a html document:
    
    <iframe src="https://dartpad.dartlang.org/embed-html.html?id=72d83fe97bfc8e735607&verticalRatio=80></iframe>

Specify the width and the height as style parameters of the iframe:
    
    <iframe style="width:400px;height:400px" src="https://dartpad.dartlang.org/embed-html.html&id=72d83fe97bfc8e735607&verticalRatio=80></iframe>

In this URL, we have the query ending
?id=72d83fe97bfc8e735607&verticalRatio=80 added path.
This means that our servers will show a gist with the hashed ID 72d83fe97bfc8e735607
Found at [https://gist.github.com/devoncarew/72d83fe97bfc8e735607](https://gist.github.com/devoncarew/72d83fe97bfc8e735607), and vertical splitters with ratios of 80%:20%.

To add multiple queries, simply separate them by the "&" (ampersand) symbol.

**List of Query Elements**

id (gist ID)  
verticalRatio (0 to 100) [Embed only]  
horizontalRatio(0 to 100) [Embed only]