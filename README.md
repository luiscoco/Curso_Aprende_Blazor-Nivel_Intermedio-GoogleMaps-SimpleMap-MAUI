# How to show a Google Map in a MAUI Blazor application

In this sample we are going to create a MAUI Blazor Application with Visual Studio 2022

We will create a Razor component to invoke the GoogleMap API to show a simple map

**Note**: for getting more information about GoogleMaps API in JavaScript visit this example in the URL

https://developers.google.com/maps/documentation/javascript/examples/map-simple

## 1. We create a MAUI Blazor App with Visual Studio 2022 Community Edition

Install Visual Studio 2022 Versión 17.12.0 Preview 2.0 Community Edition

Run Visual Studio and create a new project:

![image](https://github.com/user-attachments/assets/55158bf9-11cf-4e69-9e12-f6911cbae56b)

We select **MAUI Blazor** project template: 

![image](https://github.com/user-attachments/assets/34bebd43-6c58-4c64-b7c5-5be010a79658)

We set the project name and location in the hard disk:

![image](https://github.com/user-attachments/assets/dddf0fd6-1812-4bf1-bdbc-ac8d31eb6c74)

We leave all the default values for the following options and press the Create button

![image](https://github.com/user-attachments/assets/97840e1c-2370-48b9-ac97-565e643c84a9)

See the project folders and files structure

![image](https://github.com/user-attachments/assets/0572c39c-562f-47d1-b28a-47f4d8c99a3d)

## 2. We create a GoogleMap API Key in the Google Cloud Console

We navigate to the Google Cloud Console and we login

https://cloud.google.com/cloud-console

We press in the Console button to login 

![image](https://github.com/user-attachments/assets/ee22472f-4a50-4f10-af8a-cabc4dbf55e9)

We expand the menu and we select **APIs and Services** menu option

![image](https://github.com/user-attachments/assets/a0c99814-4474-45e3-9893-5209007c63b5)

We create a new API Key

![image](https://github.com/user-attachments/assets/e0b9741a-676b-4b89-acf0-a4797b90b3a3)

We copy the API Key code from the GoogleCloud console

![image](https://github.com/user-attachments/assets/ccb46f74-2957-47b6-84bc-6ba495ba8d86)

And we paste this code in the **index.html** component

![image](https://github.com/user-attachments/assets/ccb3476e-65c9-4dd3-9509-985c2b3dfe39)

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="utf-8" />
    <meta name="viewport" content="width=device-width, initial-scale=1.0, maximum-scale=1.0, user-scalable=no, viewport-fit=cover" />
    <title>MAUI_GoogleMaps_SimpleMap</title>
    <base href="/" />
    <link rel="stylesheet" href="css/bootstrap/bootstrap.min.css" />
    <link rel="stylesheet" href="css/app.css" />
    <link rel="stylesheet" href="MAUI_GoogleMaps_SimpleMap.styles.css" />
    <link rel="icon" href="data:,">
</head>

<body>
    <div class="status-bar-safe-area"></div>
    <div id="app">Loading...</div>
    <div id="blazor-error-ui">
        An unhandled error has occurred.
        <a href="" class="reload">Reload</a>
        <a class="dismiss">🗙</a>
    </div>
    <script src="_framework/blazor.webview.js" autostart="false"></script>
    <script src="https://maps.googleapis.com/maps/api/js?key=XXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXX"
            defer></script>
    <script src="googlemaps.js"></script>
</body>

</html>
```

## 3. We create the JavaScript function for invoking the GoogleMap API

We create a new JavaScript file inside wwwroot folder

![image](https://github.com/user-attachments/assets/4f5f3d90-b4a8-43a8-8e8e-bbe7fb1b1930)

We type the JavaScript code in the **googlemaps.js** file: 

```JavaScript
let map;

async function initMap() {
    const { Map } = await google.maps.importLibrary("maps");

    map = new Map(document.getElementById("map"), {
        center: { lat: -34.397, lng: 150.644 },
        zoom: 8,
    });
}

initMap();
```

## 4. We include the googlemaps.js file reference in the index.html component

We include this line in the App.razor code for including the googlemaps.js file inthe Blazor Web Application

```
<script src="googlemaps.js"></script>
```

# 5. Create a new Razor Component to show the Google Map

We right click on the Pages folder and create a new component **GoogleMaps.razor**

![image](https://github.com/user-attachments/assets/db432937-06bb-492c-9dc1-815b0eec2898)

This is the new component source code:

**GoogleMaps.razor**

```razor
@page "/googleMaps"

@inject IJSRuntime JSRuntime

<h3>Google Maps with Geolocation</h3>

<!-- Map container -->
<div id="map-container">
    <div id="map" style="height: 400px; width: 100%;"></div>
</div>

<!-- Button to trigger geolocation and center the map -->
<button class="btn btn-primary" @onclick="PanToCurrentLocation">Pan to Current Location</button>

@code {
    private async Task PanToCurrentLocation()
    {
        await JSRuntime.InvokeVoidAsync("initMap");
    }
}
```

## 6. Create a new menu item in the NavMenu.razor component

We open the NavMenu.razor component and we create a new NavLink item for navigating to the new component

```razor
<div class="nav-item px-3">
     <NavLink class="nav-link" href="googleMaps">
          <span class="bi bi-list-nested-nav-menu" aria-hidden="true"></span> GoogleMaps
     </NavLink>
</div>
```

## 7. Run the Blazor MAUI application in Windows Desktop

![image](https://github.com/user-attachments/assets/01e6e98b-7d91-452e-a871-11c34edd4fd6)

![image](https://github.com/user-attachments/assets/6f5dd6ca-7f02-4899-ab15-a0d669ebcefc)

![image](https://github.com/user-attachments/assets/af00085e-3df5-4344-a814-86236a0f98c9)

![image](https://github.com/user-attachments/assets/a4dccf5d-5658-4755-96b4-7858820e0104)

## 8. Run the Blazor MAUI application in your Mobile Device

Prior to run your application in your Mobile you have to connect the Mobile to your Laptop with a USB wire

Also in Visual Studio 2022 Community Edition you have to navigate to the menu option **Compile->Configurations Manager...** and select the checkbox **Implement**

![image](https://github.com/user-attachments/assets/c7d5df04-880f-4a8c-8e49-1ddc507f84c2)

![image](https://github.com/user-attachments/assets/f663aa50-bf93-4b86-8baf-7af7270aa8ca)

Now you have to check your mobile is connected to your laptop running this command:

```
adb devices
```

![image](https://github.com/user-attachments/assets/c61fb3f1-0559-4068-af74-77a69b343a64)

Then you have to select your Mobile in the **Android Local Devices** menu option 

![image](https://github.com/user-attachments/assets/e9759283-fb5a-4d8b-b4bf-ecca94c5cf63)

Then press the run button 

![image](https://github.com/user-attachments/assets/f4d03226-af16-4a3f-b93b-2f70fc75065d)

And see your MAUI application running in your Mobile and also in Visual Studio IDE

![image](https://github.com/user-attachments/assets/1675cd66-e9aa-4e9c-955a-77230fbf6287)

![image](https://github.com/user-attachments/assets/928b21be-122d-4245-8b1d-84a9ec67b32a)

![image](https://github.com/user-attachments/assets/78a3b4b1-01f9-48f7-9587-790354e0fb77)

