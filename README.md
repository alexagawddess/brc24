# BRC24D - Layered Dynamic Random Image Display using HTML files

Version: 1.0

Date: July 4, 2023

Author: Alexa Milazzo

Status: Final

**1. Overview**

BRC24D describes a method for displaying layers of random images from predefined sets of images inscribed to the Bitcoin Blockchain, where each layer's image is updated dynamically at fixed intervals (for example, every 5 minutes). This protocol extends by adding a layering capability using HTML files and iframes.

**2. Requirements**

- HTML files that access a set of predetermined images.
- JavaScript must be enabled in the browser for the dynamic update of images.
- The images must be accessible to the HTML files via valid URIs or local relative paths.

**3. Implementation**

This protocol involves two main steps: creating individual HTML files that each display a changing image, and creating a master HTML file that layers these individual files using iframes.

**3.1 Individual HTML Files**

- Create an HTML file with an img element. Assign this element a unique Inscription ID.
- Include a JavaScript function in the HTML file that selects a random image from a predefined Inscription ID and sets it as the source of the img element.
- When the page loads, call the JavaScript function immediately to display a random Inscription ID. Also set the function to be called again at the desired interval using JavaScript's setInterval() function.
 
**3.2 Master HTML File**

- Create a new HTML file. This will be your main file.
- In the body of this file, create a div that will serve as a container for several iframe elements.
- Create an iframe for each of the individual HTML files you created in step 3.1. Set the src attribute of each iframe to point to one of these individual files.
- Apply CSS to position the iframe elements so they overlap each other and create a layered effect. This can be achieved by setting the position property of each iframe to absolute.
  
**4. Code Example**

**INDIVIDUAL HTML FILES**
```
<!DOCTYPE html>
<html>
<head>
    <script>
        window.onload = function() {
            var images = [
                '/content/INSCRIPTION ID', '/content/INSCRIPTION ID', '/content/INSCRIPTION ID'
                // add more paths for images for this layer
            ];

            function updateImage(imgElementId) {
                var index = Math.floor(Math.random() * images.length);
                document.getElementById(imgElementId).src = images[index];
            }

            updateImage('dynamicImage');

            setInterval(function() {
                updateImage('dynamicImage');
            }, 5 * 60 * 1000);
        };
    </script>
</head>
<body>
    <img id="dynamicImage" src="" alt="Dynamic Image">
</body>
</html>```

**MASTER HTML FILE**
```
<!DOCTYPE html>
<html>
<head>
    <style>
        /* Centering the container */
        body {
            display: flex;
            justify-content: center;
            align-items: center;
            height: 100vh;
            margin: 0;
            padding: 0;
            overflow: hidden;
        }

        /* Setting the size of the iframe */
        .layered-content > iframe {
            position: absolute;
            height: 100%;
            width: 100%;
            border: 0; /* Remove border from iframe */
        }
    </style>
</head>
<body>
    <div class="layered-content">
        <iframe src="/content/INSCRIPTIONID"></iframe>
        <iframe src="/content/INSCRIPTIONID"></iframe>
        <iframe src="/content/INSCRIPTIONID"></iframe>
        <!-- Add more iframes as per your requirement -->
    </div>
</body>
</html>
```
**5. Customization**

Users of the BRC24D protocol may customize the list of images, the ID of the HTML img element, the interval between image changes, and the positioning and styling of the iframe elements, according to the needs of their specific application.

**6. Limitations and Considerations**

- This protocol relies on JavaScript, which must be enabled in the viewer's web browser. The functionality will not work in browsers with JavaScript disabled.
- This protocol assumes the images are accessible and loadable by the web browser. Image files that are too large may take a noticeable amount of time to load, or may fail to load entirely, depending on the viewer's internet connection.
- Cross-origin restrictions may prevent iframes from displaying content from different domains. Ensure that all files are hosted on the same domain or that proper CORS (Cross-Origin Resource Sharing) policies are in place.
- This protocol provides guidelines for the implementation of a layered, dynamic, random image display using HTML files and iframes. It can be adapted and customized according to the user's needs.
