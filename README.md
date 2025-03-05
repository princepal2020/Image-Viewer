# Image-Viewer
Image View  propeties according

<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Image Orientation Detection</title>
    <style>
        * {
            margin: 0;
            padding: 0;
            box-sizing: border-box;
        }
        body {
            display: flex;
            flex-direction: column;
            justify-content: center;
            align-items: center;
            height: 100vh;
            background-color: #f4f4f4;
            overflow: hidden;
            text-align: center;
        }
        input {
            margin-bottom: 20px;
        }
        .image-container {
            display: flex;
            justify-content: center;
            align-items: center;
            width: 80vw;
            height: 60vh;
            max-width: 600px;
            max-height: 400px;
            overflow: hidden;
            border: 4px solid transparent;
            background-color: white;
        }
        img {
            max-width: 100%;
            max-height: 100%;
            display: none;
            transition: 0.3s;
        }
        .landscape {
            border-color: green;
        }
        .portrait {
            border-color: blue;
        }
        .square {
            border-color: orange;
        }
    </style>
</head>
<body>

    <input type="file" id="fileInput" accept="image/*">
    <p id="orientationText"></p>
    <div class="image-container">
        <img id="imagePreview" src="https://media.istockphoto.com/id/1335941248/photo/shot-of-a-handsome-young-man-standing-against-a-grey-background.jpg?s=612x612&w=0&k=20&c=JSBpwVFm8vz23PZ44Rjn728NwmMtBa_DYL7qxrEWr38=">
    </div>

    <script>
        document.getElementById("fileInput").addEventListener("change", function(event) {
            const file = event.target.files[0];
            if (file) {
                const reader = new FileReader();
                reader.onload = function(e) {
                    const img = new Image();
                    img.src = e.target.result;

                    img.onload = function() {
                        const imagePreview = document.getElementById("imagePreview");
                        const orientationText = document.getElementById("orientationText");
                        const container = document.querySelector(".image-container");

                        imagePreview.src = img.src;
                        imagePreview.style.display = "block";

                        // Remove previous classes
                        container.classList.remove("landscape", "portrait", "square");

                        // Check orientation
                        if (img.naturalWidth > img.naturalHeight) {
                            orientationText.innerText = "Landscape View";
                            container.classList.add("landscape");
                        } else if (img.naturalWidth < img.naturalHeight) {
                            orientationText.innerText = "Portrait View";
                            container.classList.add("portrait");
                        } else {
                            orientationText.innerText = "Square Image";
                            container.classList.add("square");
                        }
                    };
                };
                reader.readAsDataURL(file);
            }
        });
    </script>

</body>
</html>
------------------------------------------------------  on Popup full screen according image  -------------------------------------------------------------
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Image Orientation Modal</title>
    <style>
        * {
            margin: 0;
            padding: 0;
            box-sizing: border-box;
        }
        body {
            display: flex;
            flex-direction: column;
            justify-content: center;
            align-items: center;
            height: 100vh;
            background-color: #f4f4f4;
            overflow: hidden;
            text-align: center;
        }
        input {
            margin-bottom: 20px;
        }
        
        /* Modal Styles */
        .modal {
            display: none; 
            position: fixed;
            top: 0;
            left: 0;
            width: 100%;
            height: 100%;
            background: rgba(0, 0, 0, 0.8);
            justify-content: center;
            align-items: center;
        }
        .modal-content {
            position: relative;
            width: 600px;  /* Fixed width */
            height: 400px; /* Fixed height */
            background: white;
            border-radius: 10px;
            display: flex;
            flex-direction: column;
            align-items: center;
            justify-content: center;
            padding: 20px;
        }
        .modal img {
            max-width: 90%;  /* Ensures it fits inside */
            max-height: 90%; /* Maintains aspect ratio */
            border: 4px solid transparent;
        }
        .landscape {
            border-color: green;
        }
        .portrait {
            border-color: blue;
        }
        .square {
            border-color: orange;
        }
        .close {
            position: absolute;
            top: 10px;
            right: 15px;
            font-size: 24px;
            cursor: pointer;
            color: red;
        }
    </style>
</head>
<body>

    <input type="file" id="fileInput" accept="image/*">
    <p id="orientationText"></p>

    <!-- Modal -->
    <div id="imageModal" class="modal">
        <div class="modal-content">
            <span class="close">&times;</span>
            <p id="modalOrientationText"></p>
            <img id="modalImage">
        </div>
    </div>

    <script>
        const fileInput = document.getElementById("fileInput");
        const modal = document.getElementById("imageModal");
        const modalImage = document.getElementById("modalImage");
        const modalOrientationText = document.getElementById("modalOrientationText");
        const closeModal = document.querySelector(".close");

        fileInput.addEventListener("change", function(event) {
            const file = event.target.files[0];
            if (file) {
                const reader = new FileReader();
                reader.onload = function(e) {
                    const img = new Image();
                    img.src = e.target.result;

                    img.onload = function() {
                        modalImage.src = img.src;

                        // Remove previous classes
                        modalImage.classList.remove("landscape", "portrait", "square");

                        // Check orientation
                        if (img.naturalWidth > img.naturalHeight) {
                            modalOrientationText.innerText = "Landscape View";
                            modalImage.classList.add("landscape");
                        } else if (img.naturalWidth < img.naturalHeight) {
                            modalOrientationText.innerText = "Portrait View";
                            modalImage.classList.add("portrait");
                        } else {
                            modalOrientationText.innerText = "Square Image";
                            modalImage.classList.add("square");
                        }

                        // Show modal
                        modal.style.display = "flex";
                    };
                };
                reader.readAsDataURL(file);
            }
        });

        // Close modal when clicking the close button
        closeModal.addEventListener("click", function() {
            modal.style.display = "none";
        });

        // Close modal when clicking outside the modal content
        window.addEventListener("click", function(event) {
            if (event.target === modal) {
                modal.style.display = "none";
            }
        });
    </script>

</body>
</html>
------------------------------------------------------------------------------------------  popup auto height width -------------------------
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Image Orientation Modal</title>
    <style>
        * {
            margin: 0;
            padding: 0;
            box-sizing: border-box;
        }
        body {
            display: flex;
            flex-direction: column;
            justify-content: center;
            align-items: center;
            height: 100vh;
            background-color: #f4f4f4;
            overflow: hidden;
            text-align: center;
        }
        input {
            margin-bottom: 20px;
        }
        
        /* Modal Styles */
        .modal {
            display: none; 
            position: fixed;
            top: 0;
            left: 0;
            width: 100%;
            height: 100%;
            background: rgba(0, 0, 0, 0.8);
            justify-content: center;
            align-items: center;
        }
        .modal-content {
            position: relative;
            max-width: 80vw;
            max-height: 80vh;
            padding: 20px;
            background: white;
            border-radius: 10px;
            display: flex;
            flex-direction: column;
            align-items: center;
        }
        .modal img {
            max-width: 100%;
            max-height: 60vh;
            border: 4px solid transparent;
        }
        .landscape {
            border-color: green;
        }
        .portrait {
            border-color: blue;
        }
        .square {
            border-color: orange;
        }
        .close {
            position: absolute;
            top: 10px;
            right: 15px;
            font-size: 24px;
            cursor: pointer;
            color: red;
        }
    </style>
</head>
<body>

    <input type="file" id="fileInput" accept="image/*">
    <p id="orientationText"></p>

    <!-- Modal -->
    <div id="imageModal" class="modal">
        <div class="modal-content">
            <span class="close">&times;</span>
            <p id="modalOrientationText"></p>
            <img id="modalImage">
        </div>
    </div>

    <script>
        const fileInput = document.getElementById("fileInput");
        const modal = document.getElementById("imageModal");
        const modalImage = document.getElementById("modalImage");
        const modalOrientationText = document.getElementById("modalOrientationText");
        const closeModal = document.querySelector(".close");

        fileInput.addEventListener("change", function(event) {
            const file = event.target.files[0];
            if (file) {
                const reader = new FileReader();
                reader.onload = function(e) {
                    const img = new Image();
                    img.src = e.target.result;

                    img.onload = function() {
                        modalImage.src = img.src;

                        // Remove previous classes
                        modalImage.classList.remove("landscape", "portrait", "square");

                        // Check orientation
                        if (img.naturalWidth > img.naturalHeight) {
                            modalOrientationText.innerText = "Landscape View";
                            modalImage.classList.add("landscape");
                        } else if (img.naturalWidth < img.naturalHeight) {
                            modalOrientationText.innerText = "Portrait View";
                            modalImage.classList.add("portrait");
                        } else {
                            modalOrientationText.innerText = "Square Image";
                            modalImage.classList.add("square");
                        }

                        // Show modal
                        modal.style.display = "flex";
                    };
                };
                reader.readAsDataURL(file);
            }
        });

        // Close modal when clicking the close button
        closeModal.addEventListener("click", function() {
            modal.style.display = "none";
        });

        // Close modal when clicking outside the modal content
        window.addEventListener("click", function(event) {
            if (event.target === modal) {
                modal.style.display = "none";
            }
        });
    </script>

</body>
</html>



