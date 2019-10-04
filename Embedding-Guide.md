### Embedding Snippets

**So, you want to embed a code snippet into your website?**
No worries, it's simple! 

DartPad offers 4 different embedding choices for shared code. You have the option to show:

1. Dart and console [embed-dart.html](#embed-dart.html)
3. Dart and console (minimal) [embed-inline](#embed-inline.html)
3. Flutter, console, and HTML output [embed-flutter](#embed-flutter.html)
4. Dart, console, and HTML output (with options to modify HTML/CSS) [embed-html](#embed-html.html)

DartPad pages use query parameters in the URL to retrieve & show certain information.
This means that users can configure how to show their code by quickly changing the URL.

A sample URL would be 
[https://dartpad.dev/embed-inline.html?id=5d70bc1889d055c7a18d35d77874af88&split=80&theme=dark](https://dartpad.dev/embed-inline.html?id=5d70bc1889d055c7a18d35d77874af88&split=80&theme=dark)

It can be embedded by inserting the following code into a html document:
    
    <iframe src="https://dartpad.dev/embed-html.html?id=72d83fe97bfc8e735607&split=80&theme=dark></iframe>

Specify the width and the height as style parameters of the iframe:
    
    <iframe style="width:400px;height:400px;" src="https://dartpad.dev/embed-html.html&id=72d83fe97bfc8e735607&split=80&theme=dark></iframe>

In this URL, we have the query ending
`?id=72d83fe97bfc8e735607&split=80` added path.
This means that our servers will show a gist with the hashed ID `72d83fe97bfc8e735607`
Found at [https://gist.github.com/devoncarew/72d83fe97bfc8e735607](https://gist.github.com/devoncarew/72d83fe97bfc8e735607), and vertical splitters with ratios of 80%:20%.

To add multiple query parameters, simply separate them by the "&" (ampersand) symbol.

#### embed-dart.html

A simple interface for Dart code that includes an editor and console on the righthand side.

<img width="945" alt="Screen Shot 2019-07-25 at 1 39 21 PM" src="https://user-images.githubusercontent.com/969662/61907271-01599200-aee2-11e9-9c68-4b874f8937e1.png">

#### embed-inline.html

Another simple interface for Dart code with a console beneath the editor.

<img width="942" alt="Screen Shot 2019-07-25 at 9 41 17 PM" src="https://user-images.githubusercontent.com/969662/61926324-fecc5c00-af24-11e9-9971-9de427699dcb.png">

#### embed-flutter.html

A layout for editing and running Flutter code. When this layout is used, code is
compiled with DDC rather than dart2js, and the Flutter for web packages are available
for import.

<img width="948" alt="Screen Shot 2019-07-25 at 1 39 36 PM" src="https://user-images.githubusercontent.com/969662/61907277-03235580-aee2-11e9-8940-082322197791.png">

#### embed-html.html

A layout for editing `dart:html` projects. Editors for HTML, CSS, and Dart are included,
and HTML output is displayed to the right.

<img width="949" alt="Screen Shot 2019-07-25 at 1 41 10 PM" src="https://user-images.githubusercontent.com/969662/61907279-04ed1900-aee2-11e9-933e-d8552663b0ed.png">

See the experimental embeddings [demo page](https://dartpad.dev/experimental/new_embeddings_demo.html) for 
live examples of each format.

### List of query elements

The experimental embed UI looks for these parameters in its query string:

* **id**: ID of a GitHub gist to load into the editor
* **split**: Percentage of the iframe width to use for the editor (the rest may be used by the console or Flutter/HTML output).
* **theme**: Set this to 'dark' to use the dark theme (seen in the first screenshot above).

Embedded views exported in strong mode will land in the main dartpad web client with strong mode enabled.

### Styling the editor

Right now, the embedded editor will style its own contents according to the desired theme (either light or dark). No border is added to the iframe contents by DartPad, nor does it attempt to size itself. Developers adding DartPad iframes to their pages should use CSS within their own pages to style these properties.

### Testing the user's code

In addition to running code and displaying the output, the new embed UI can present exercises to be completed by the user and then test their responses. It does this by combining the user's code with additional "test" code provided by the exercise author and executing the result as if it were a single file. 

An example exercise might look like this:

**User's code**
```dart
String stringify(int x, int y) {
  return '$x $y';
}
```

**Test code**
```dart
void main() {
  try {
    final str = stringify(2, 3); 

    if (str == '2 3') {
      _result(true);
    } else if (str == '23') {
      _result(false, ['Test failed. It looks like you forgot the space!']);
    } else if (str == null) {
      _result(false, ['Test failed. Did you forget to return a value?']);
    } else {
      _result(false, ['That\'s not quite right. Keep trying!']);
    }
  } catch (e) {
    _result(false, ['Tried calling stringify(2, 3), but received an exception: ${e.runtimeType}']);
  }
}
```

When combined and executed, the `main` method present in the test code runs, calls into the user's code, and validates the result. The `_result` function is provided by DartPad in the scope in which the test code executes and can be used to report the result of a test. It takes a single boolean indicating success or failure, and a list of strings to be displayed to the user with the result.

### Testing the user's code

GitHub gists can be loaded into the new embed UI automatically by appending `id=[Gist ID]` to the end of the query string. The embed will look for the following files within a gist:

* **main.dart**: The starting state for the user's code (an unfinished method, for example).
* **test.dart**: A `main` that will test the above code, along with any classes, functions, constants, etc. that will be used in the process.
* **solution.dart**: The ideal solution to the exercise (i.e. what main.dart would look like after being successfully completed by the user).
* **hint.txt**: A text hint that can be displayed to the user when requested, and which will help them complete the exercise ("Try X or Y," "Have you considered Z," etc.).
 
