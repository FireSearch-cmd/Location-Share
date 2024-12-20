<!DOCTYPE html>
<html>
<head>
    <title>Share Your Location</title>
    <script>
        function getLocation() {
            if (navigator.geolocation) {
                navigator.geolocation.getCurrentPosition(sendLocation, showError);
            } else {
                alert("Geolocation is not supported by this browser.");
            }
        }

        function sendLocation(position) {
            const lat = position.coords.latitude;
            const lon = position.coords.longitude;

            // Send the location to your server (replace URL with your server's endpoint)
            fetch('https://your-server-endpoint.com/location', {
                method: 'POST',
                headers: {
                    'Content-Type': 'application/json'
                },
                body: JSON.stringify({ latitude: lat, longitude: lon })
            });

            // Show confirmation
            document.getElementById("message").innerHTML = "Your location has been shared!";
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
