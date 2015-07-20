DartPad pages use query parameters in the URL to retrieve & show certain information.
This means that users can configure how to show their code by quickly changing the URL.

A sample URL would be 
[https://dartpad.dartlang.org/embed-dart.html?id=72d83fe97bfc8e735607&verticalRatio=80](https://dartpad.dartlang.org/embed-dart.html?id=72d83fe97bfc8e735607&verticalRatio=80)

In this URL, we have the query ending
?id=72d83fe97bfc8e735607&verticalRatio=80 added path.
This means that our servers will show a gist with the hashed ID 72d83fe97bfc8e735607
Found at [https://gist.github.com/devoncarew/72d83fe97bfc8e735607](https://gist.github.com/devoncarew/72d83fe97bfc8e735607), and vertical splitters with ratios of 80%:20%.

To add multiple queries, simply separate them by the "&" (ampersand) symbol.

List of Query Elements and their values:  
id (gist ID)  
verticalRatio (0 to 100) [Embed only]  
horizontalRatio(0 to 100) [Embed only]  