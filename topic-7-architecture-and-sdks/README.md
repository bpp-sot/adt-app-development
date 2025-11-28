# Topic 7 Practical: Integrating an SDK

## Overview

In this practical, you will integrate a third-party SDK into your React application. This exercise demonstrates the process of evaluating, installing, and implementing external libraries—a core skill for any software engineer.

By the end of this practical, you will have:

- Installed an SDK using npm (Node Package Manager)
- Initialised and configured the SDK within your application
- Implemented a basic feature using the SDK
- Documented your integration process through commits
- Evaluated the SDK against professional criteria

This practical directly supports your portfolio evidence for **K26** (selecting and applying software tools) and **S19** (implementing software engineering projects using appropriate methods and techniques).

---

## Prerequisites

Before starting this practical, ensure you have:

- Completed the base repository setup (your React app should be running)
- Your Codespace open with the terminal available
- The development server running (`npm run dev`)

If your development server is not running, start it now:

```bash
npm run dev
```

You should see output indicating the server is running at `http://localhost:5173`.

---

## The Scenario

Recall the "Local Event Finder" app from Practical 1. A mapping feature would be essential for this application—users need to see where events are located. You will now integrate a mapping SDK to provide this functionality.

---

## Part 1: Choosing Your SDK

For this practical, you will integrate **Leaflet**, an open-source JavaScript library for interactive maps. Leaflet is widely used in production applications and provides an excellent example of SDK integration.

### Why Leaflet?

Before integrating any SDK, you should evaluate it against your requirements. Consider:

| Criterion | Leaflet Assessment |
|-----------|-------------------|
| **Functionality** | Provides interactive maps, markers, popups, and geolocation |
| **Licensing** | BSD 2-Clause (permissive, suitable for commercial use) |
| **Documentation** | Comprehensive, with tutorials and API reference |
| **Community** | Large, active community with regular updates |
| **Size** | Lightweight (~42KB gzipped) |
| **Dependencies** | None (standalone library) |

---

## Part 2: Installing the SDK

### Step 1: Install the packages

Open your terminal in Codespaces and run the following command:

```bash
npm install leaflet react-leaflet
```

This installs two packages:

- **leaflet**: The core mapping library
- **react-leaflet**: React components that wrap Leaflet for easier integration

### Step 2: Verify the installation

Check your `package.json` file. You should see both packages listed under `dependencies`:

```json
"dependencies": {
  "leaflet": "^1.9.x",
  "react": "^18.x.x",
  "react-dom": "^18.x.x",
  "react-leaflet": "^4.x.x"
}
```

> **Note**: Version numbers may differ slightly—this is normal.

### Step 3: Commit your changes

Make your first commit to document the SDK installation:

```bash
git add package.json package-lock.json
git commit -m "Add Leaflet and react-leaflet dependencies for mapping feature"
```

---

## Part 3: Creating the Map Component

### Step 1: Create the components folder

If it doesn't already exist, create a `components` folder inside `src`:

```bash
mkdir -p src/components
```

### Step 2: Create the Map component

Create a new file called `Map.jsx` inside `src/components/`:

```bash
touch src/components/Map.jsx
```

Open the file and add the following code:

```jsx
import { MapContainer, TileLayer, Marker, Popup } from 'react-leaflet';
import 'leaflet/dist/leaflet.css';

// Fix for default marker icons in React-Leaflet
import L from 'leaflet';
import markerIcon2x from 'leaflet/dist/images/marker-icon-2x.png';
import markerIcon from 'leaflet/dist/images/marker-icon.png';
import markerShadow from 'leaflet/dist/images/marker-shadow.png';

delete L.Icon.Default.prototype._getIconUrl;
L.Icon.Default.mergeOptions({
  iconRetinaUrl: markerIcon2x,
  iconUrl: markerIcon,
  shadowUrl: markerShadow,
});

function Map() {
  // Default position: Central London
  const position = [51.5074, -0.1278];

  // Sample events for the Local Event Finder
  const events = [
    {
      id: 1,
      name: 'Tech Meetup',
      position: [51.5074, -0.1278],
      description: 'Monthly technology networking event',
    },
    {
      id: 2,
      name: 'Code Workshop',
      position: [51.5194, -0.1270],
      description: 'Hands-on programming workshop',
    },
    {
      id: 3,
      name: 'Design Conference',
      position: [51.5014, -0.1419],
      description: 'Annual UX/UI design conference',
    },
  ];

  return (
    <div className="map-wrapper">
      <MapContainer
        center={position}
        zoom={13}
        style={{ height: '500px', width: '100%' }}
      >
        <TileLayer
          attribution='&copy; <a href="https://www.openstreetmap.org/copyright">OpenStreetMap</a> contributors'
          url="https://{s}.tile.openstreetmap.org/{z}/{x}/{y}.png"
        />
        {events.map((event) => (
          <Marker key={event.id} position={event.position}>
            <Popup>
              <strong>{event.name}</strong>
              <br />
              {event.description}
            </Popup>
          </Marker>
        ))}
      </MapContainer>
    </div>
  );
}

export default Map;
```

### Understanding the code

Let's break down what this component does:

1. **Imports**: We import the necessary components from `react-leaflet` and the CSS styles from `leaflet`.

2. **Icon fix**: React-Leaflet has a known issue with default marker icons. The icon configuration block resolves this.

3. **Position data**: We define coordinates using latitude and longitude arrays.

4. **Sample events**: An array of event objects demonstrates how real data might be structured.

5. **MapContainer**: The main wrapper component that initialises the map.

6. **TileLayer**: Provides the map imagery from OpenStreetMap (free, no API key required).

7. **Markers and Popups**: Display event locations with interactive information popups.

### Step 3: Commit the component

```bash
git add src/components/Map.jsx
git commit -m "Create Map component with Leaflet integration and sample events"
```

---

## Part 4: Integrating the Component

### Step 1: Update App.jsx

Open `src/App.jsx` and replace its contents with:

```jsx
import Map from './components/Map';
import './App.css';

function App() {
  return (
    <div className="app">
      <header className="app-header">
        <h1>Local Event Finder</h1>
        <p>Discover events happening near you</p>
      </header>
      <main className="app-main">
        <Map />
      </main>
    </div>
  );
}

export default App;
```

### Step 2: Add basic styling

Open `src/App.css` and replace its contents with:

```css
.app {
  font-family: -apple-system, BlinkMacSystemFont, 'Segoe UI', Roboto, Oxygen,
    Ubuntu, Cantarell, sans-serif;
  max-width: 1200px;
  margin: 0 auto;
  padding: 20px;
}

.app-header {
  text-align: center;
  margin-bottom: 30px;
}

.app-header h1 {
  color: #2c3e50;
  margin-bottom: 10px;
}

.app-header p {
  color: #7f8c8d;
  font-size: 1.1rem;
}

.app-main {
  border-radius: 8px;
  overflow: hidden;
  box-shadow: 0 4px 6px rgba(0, 0, 0, 0.1);
}

.map-wrapper {
  width: 100%;
}
```

### Step 3: Test your application

Your development server should automatically reload. If not, check the terminal for errors.

You should see:

- A header with "Local Event Finder"
- An interactive map of Central London
- Three markers indicating sample events
- Clickable popups showing event details

### Step 4: Commit the integration

```bash
git add src/App.jsx src/App.css
git commit -m "Integrate Map component into main application with styling"
```

---

## Part 5: Extending the Feature (Optional Enhancement)

If time permits, try adding one of these enhancements:

### Option A: Add your current location

Add this import at the top of `Map.jsx`:

```jsx
import { useEffect, useState } from 'react';
```

Then modify the component to detect the user's location:

```jsx
function Map() {
  const [userPosition, setUserPosition] = useState(null);
  const defaultPosition = [51.5074, -0.1278];

  useEffect(() => {
    if ('geolocation' in navigator) {
      navigator.geolocation.getCurrentPosition(
        (position) => {
          setUserPosition([
            position.coords.latitude,
            position.coords.longitude,
          ]);
        },
        (error) => {
          console.log('Geolocation error:', error.message);
        }
      );
    }
  }, []);

  const mapCenter = userPosition || defaultPosition;

  // ... rest of component
}
```

### Option B: Add a custom marker colour

Create a custom icon for different event types:

```jsx
const customIcon = new L.Icon({
  iconUrl: 'https://raw.githubusercontent.com/pointhi/leaflet-color-markers/master/img/marker-icon-2x-red.png',
  shadowUrl: 'https://cdnjs.cloudflare.com/ajax/libs/leaflet/1.7.1/images/marker-shadow.png',
  iconSize: [25, 41],
  iconAnchor: [12, 41],
  popupAnchor: [1, -34],
  shadowSize: [41, 41],
});
```

If you complete an enhancement, commit your changes:

```bash
git add -A
git commit -m "Add [description of your enhancement]"
```

---

## Part 6: Capturing Evidence

For your portfolio, you need to capture the following evidence:

### Screenshot 1: Working application

Take a screenshot showing:

- The map displayed in your browser
- At least one popup open showing event details
- The URL bar showing your Codespace address

### Screenshot 2: Package.json dependencies

Take a screenshot of your `package.json` file showing the Leaflet dependencies.

### Screenshot 3: Commit history

In your terminal, run:

```bash
git log --oneline
```

Take a screenshot showing your commit history with meaningful messages.

Alternatively, view your commit history on GitHub:

1. Go to your repository on GitHub
2. Click on "Commits"
3. Screenshot the commit history

---

## Part 7: SDK Evaluation

In your Development Log, answer the following evaluation questions. These form part of your portfolio evidence.

### Evaluation Questions

1. **Requirements fit**: Does Leaflet meet the mapping requirements for the Local Event Finder app? What features does it provide that you would use? What might be missing?

2. **Integration complexity**: How easy was it to integrate Leaflet into your React application? What challenges did you encounter? How did the documentation help (or not)?

3. **Performance considerations**: Did you notice any impact on application load time or responsiveness? How might this affect user experience on mobile devices?

4. **Licensing implications**: Leaflet uses the BSD 2-Clause licence. What does this mean for a commercial application? Are there any restrictions you need to be aware of?

5. **Production recommendation**: Would you recommend keeping Leaflet in a production version of this application? Justify your answer with specific reasons.

### Reflection Prompt

Consider how your chosen architecture (from Practical 1) supports or limits the use of this SDK. For example:

- Where does the Map component sit in your architecture layers?
- How would you handle map-related state in an MVVM pattern?
- What would change if you needed to swap Leaflet for a different mapping SDK?

---

## Submission Checklist

Before finishing, ensure you have:

- [ ] Installed Leaflet and react-leaflet packages
- [ ] Created a working Map component
- [ ] Integrated the component into your application
- [ ] Made meaningful commits at each stage
- [ ] Captured all required screenshots
- [ ] Completed the SDK evaluation questions
- [ ] Written your architecture reflection

---

## Troubleshooting

### Map not displaying

- Check the browser console for errors (F12 → Console tab)
- Ensure you imported `leaflet/dist/leaflet.css`
- Verify the MapContainer has explicit height and width styles

### Markers not showing

- Check that the icon fix code is included
- Ensure the marker positions are valid latitude/longitude arrays

### Build errors after installing packages

- Try stopping the dev server (Ctrl+C) and restarting it (`npm run dev`)
- If errors persist, delete `node_modules` and reinstall:

```bash
rm -rf node_modules
npm install
npm run dev
```

### Codespace disconnected

- Refresh the browser tab
- If the Codespace has stopped, restart it from your repository's Code menu

---

## Further Reading

- [Leaflet Documentation](https://leafletjs.com/reference.html)
- [React-Leaflet Documentation](https://react-leaflet.js.org/)
- [OpenStreetMap](https://www.openstreetmap.org/) - The free map data provider

---

## Next Steps

In the next topic, we will explore **Documentation** practices. Consider how you might document this SDK integration for other developers joining your project.

Your stretch activity for this week:

1. Refine your architecture diagram to show where the mapping SDK fits
2. Prepare a short justification for your SDK choice for next week's peer review
