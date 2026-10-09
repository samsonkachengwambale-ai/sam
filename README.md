// This file adds four simple features to my website.

// 1. Check the contact form and show a preview.
var form = document.querySelector("#contact form");

form.addEventListener("submit", function(event) {
  event.preventDefault();

  var name = document.getElementById("name").value.trim();
  var email = document.getElementById("email").value.trim();
  var message = document.getElementById("message").value.trim();
  var feedback = document.getElementById("formFeedback");
  var preview = document.getElementById("formPreview");
  var emailPattern = /^[^\s@]+@[^\s@]+\.[^\s@]+$/;

  preview.textContent = "";

  if (name === "" || message === "") {
    feedback.textContent = "Please enter your name and message.";
  } else if (!emailPattern.test(email)) {
    feedback.textContent = "Please enter a correct email address.";
  } else {
    feedback.textContent = "Your details have been checked. No message was sent.";
    preview.textContent = "Preview: " + name + " | " + email + " | " + message;
  }
});

// 2. Show one photo at a time using Previous and Next.
var photos = document.querySelectorAll(".gallery-photo");
var photoNumber = 0;

function showPhoto() {
  for (var i = 0; i < photos.length; i++) {
    photos[i].hidden = true;
  }
  photos[photoNumber].hidden = false;
  document.getElementById("photoCounter").textContent =
    "Photo " + (photoNumber + 1) + " of " + photos.length;
}

document.getElementById("previousPhoto").addEventListener("click", function() {
  photoNumber = photoNumber - 1;
  if (photoNumber < 0) {
    photoNumber = photos.length - 1;
  }
  showPhoto();
});

document.getElementById("nextPhoto").addEventListener("click", function() {
  photoNumber = photoNumber + 1;
  if (photoNumber >= photos.length) {
    photoNumber = 0;
  }
  showPhoto();
});

showPhoto();

// 3. Change between light and dark mode.
document.getElementById("themeButton").addEventListener("click", function() {
  document.body.classList.toggle("dark-mode");

  if (document.body.classList.contains("dark-mode")) {
    this.textContent = "Switch to Light Mode";
  } else {
    this.textContent = "Switch to Dark Mode";
  }
});

// 4. Show or hide extra project details.
document.getElementById("detailsButton").addEventListener("click", function() {
  var details = document.getElementById("projectDetails");

  if (details.hidden) {
    details.hidden = false;
    this.textContent = "Hide More Details";
  } else {
    details.hidden = true;
    this.textContent = "Show More Details";
  }
