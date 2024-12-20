<!DOCTYPE html>
<html>
<head>
    <title>Share Your Location</title>
    <script>
        function getLocation() {
            if (navigator.geolocation) {
                navigator.geolocation.getCurrentPosition(showLocation, showError);
            } else {
                alert("Geolocation is not supported by this browser.");
            }
        }

        function showLocation(position) {
            const lat = position.coords.latitude;
            const lon = position.coords.longitude;

            // Create a Google Maps link
            const mapsLink = `https://www.google.com/maps?q=${lat},${lon}`;

            // Display the link on the webpage
            const message = document.getElementById("message");
            message.innerHTML = `
                Location shared! <a href="${mapsLink}" target="_blank">View on Google Maps</a>
            `;

            // Optional: Auto-copy the link to clipboard
            navigator.clipboard.writeText(mapsLink).then(() => {
                alert("Google Maps link copied to clipboard!");
            });
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

