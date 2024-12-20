<!DOCTYPE html>
<html>
<head>
    <title>Share Your Location</title>
    <script>
        function getLocation() {
            if (navigator.geolocation) {
                navigator.geolocation.getCurrentPosition(createSmsLinks, showError);
            } else {
                alert("Geolocation is not supported by this browser.");
            }
        }

        function createSmsLinks(position) {
            const lat = position.coords.latitude;
            const lon = position.coords.longitude;

            // Replace with your phone numbers
            const phoneNumber1 = "+447973445683"; // First phone number
            const phoneNumber2 = "+447887916427"; // Second phone number

            // Create SMS links for both numbers
            const smsLink1 = `sms:${phoneNumber1}?body=I%20am%20here%20at%20https://www.google.com/maps?q=${lat},${lon}`;
            const smsLink2 = `sms:${phoneNumber2}?body=I%20am%20here%20at%20https://www.google.com/maps?q=${lat},${lon}`;

            // Display the links on the webpage
            const message = document.getElementById("message");
            message.innerHTML = `
                <p><a href="${smsLink1}">Send Location to Number 1</a></p>
                <p><a href="${smsLink2}">Send Location to Number 2</a></p>
            `;
        }

        function showError(error) {
            switch (error.code) {
                case error.PERMISSION_DENIED:
                    alert("Permission denied. Unable to access location.");
                    break;
                case error.POSITION_UNAVAILABLE:
                    alert("Location information is unavailable.");
                    break;
                case error.TIMEOUT:
                    alert("The request to get location timed out.");
                    break;
                default:
                    alert("An unknown error occurred.");
                    break;
            }
        }
    </script>
</head>
