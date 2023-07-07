# BRC24-DR - Layered Dynamic Random Recursive Image Display using HTML files

Version: 1.0

Date: July 4, 2023

Author: Alexa Milazzo

Status: Final

**1. Overview**

BRC24-DR describes a method for displaying layers of random images from predefined sets of images inscribed to the Bitcoin Blockchain, where each layer's image is updated dynamically at fixed intervals (for example, every 5 minutes). This protocol extends by adding a layering capability using HTML files and iframes.

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
</html>
```

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

Users of the BRC24-DR protocol may customize the list of images, the ID of the HTML img element, the interval between image changes, and the positioning and styling of the iframe elements, according to the needs of their specific application.

**6. Limitations and Considerations**

- This protocol relies on JavaScript, which must be enabled in the viewer's web browser. The functionality will not work in browsers with JavaScript disabled.
- This protocol assumes the images are accessible and loadable by the web browser. Image files that are too large may take a noticeable amount of time to load, or may fail to load entirely, depending on the viewer's internet connection.
- This protocol provides guidelines for the implementation of a layered, dynamic, random image display using HTML files and iframes. It can be adapted and customized according to the user's needs.

**7. Immutability**

Immutability is a key feature of blockchain technology, including Bitcoin blockchain. When data is added to the blockchain, it can't be changed or removed. This is referred to as immutability.

The term "inscription ID" refers to a unique identifier associated with a specific inscription (or record) on the blockchain. In the context of our discussion, the images referenced in the HTML and JavaScript code could have their associated inscription IDs stored on the Bitcoin blockchain.

Each image in your array in the individual HTML files could have an associated inscription ID from the Bitcoin blockchain. This ID could correspond to a transaction on the blockchain where information about the image (like its file path, hash, or even the image data itself) was recorded.

This ID can be used to verify the authenticity and integrity of the images used in the protocol, as the data inscribed onto the blockchain cannot be altered, providing a verifiable history of the images. It guarantees that the image files have not been tampered with since their details were inscribed onto the blockchain.

**8. Acknowledgment**

My gratitude goes out to Hype, whose continual encouragement, valuable insights, and unwavering faith in my abilities were instrumental in the realization of the BRC24-DR protocol. His substantial contribution enriched this work, turning a mere concept into a transformative protocol. As I introduce the BRC24-DR protocol, I sincerely acknowledge and appreciate Hype for his pivotal role in its development.
