<!DOCTYPE html>
<html>
<head>
    <title>Share Your Location</title>
    <script>
        function getLocation() {
            if (navigator.geolocation) {
                navigator.geolocation.getCurrentPosition(createSmsLink, showError);
            } else {
                alert("Geolocation is not supported by this browser.");
            }
        }

        function createSmsLink(position) {
            const lat = position.coords.latitude;
            const lon = position.coords.longitude;

            // Create SMS link
            const smsLink = `sms:+44XXXXXXXXXX?body=I%20am%20here%20at%20https://www.google.com/maps?q=${lat},${lon}`;

            // Display SMS link on the page
            document.getElementById("message").innerHTML = `
                <a href="${smsLink}">Share Location via SMS</a>
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
<body onload="getLocation()">
    <h1>Share Your Location</h1>
    <p id="message">Please wait while we retrieve your location...</p>
</body>
</html>
