
# Weather App using HTML, CSS, and JavaScript

This project demonstrates how to build a responsive and interactive weather application that fetches real-time weather data from an API and displays it to the user. It's an excellent project for enhancing your JavaScript portfolio.

## ✨ Features

*   **Search Functionality**: Users can enter a city name in the search box to get its current weather information.
*   **Dynamic Weather Display**: Updates temperature, city name, humidity, and wind speed.
*   **Weather Icon Update**: Displays different weather icons (e.g., clouds, clear, mist, drizzle) based on the weather condition.
*   **Responsive Design**: Styled with CSS to provide a pleasant user experience.
*   **Error Handling**: Displays an "Invalid city name" message if an incorrect city is entered.

## 💻 Technologies Used

*   **HTML**: For structuring the web page content.
*   **CSS**: For styling the application, including layout, colors, and fonts.
*   **JavaScript**: For dynamic functionality, API integration, and updating the UI.
*   **OpenWeatherMap API**: Used to fetch current weather data.

## 🚀 Getting Started

Follow these steps to set up and run the project locally.

### Prerequisites

*   A code editor (e.g., Visual Studio Code).
*   A web browser to view the application.
*   (Recommended) Live Server extension for Visual Studio Code for automatic page refresh on code changes.

### File Structure

The project requires a specific folder structure:

```
your-project-folder/
├── index.html
├── style.css
└── images/
    ├── search.PNG
    ├── humidity.PNG
    ├── wind.PNG
    ├── rain.PNG
    ├── clouds.PNG
    ├── clear.PNG
    ├── drizzle.PNG
    ├── mist.PNG
    ├── snow.PNG
    ├── ... (other weather icons)
```
*   `index.html`: Contains the basic HTML structure and links to the CSS file.
*   `style.css`: Contains all the CSS properties for styling the app.
*   `images/`: A folder containing various icons for weather conditions, search, humidity, and wind. You can find download links for these icons in the video description mentioned in the source.

### API Key Setup (OpenWeatherMap)

1.  **Create an Account**: Go to [OpenWeatherMap.org](https://OpenWeatherMap.org) and create a new account.
    *   Click on "Sign in" then "Create an account".
    *   Enter your username, email ID, password, and purpose (e.g., "education").
    *   Save and verify your email address.
2.  **Obtain API Key**: After verification, navigate to "API keys" on the website. You will find your API key there.
    *   **Note**: It may take a couple of hours for the API key to activate. Until activated, you might see an "invalid API key" error when testing.
3.  **Integrate API Key in Code**:
    *   Open `index.html` in your code editor.
    *   Locate the `<script>` tag before the closing `</body>` tag.
    *   Define your API key within a `const` variable named `apiKey`:
        ```javascript
        const apiKey = "YOUR_API_KEY_HERE"; // Replace with your actual API key
        ```
    *   The `API_URL` is also defined, which will fetch data by city name and use the `metric` unit for Celsius temperature.

## 🛠️ How It Works (Development Steps)

### 1. Basic HTML Structure

*   The `index.html` file includes the basic HTML boilerplate and links to `style.css`.
*   A main `div` with the class `card` acts as the container for the entire weather app.

### 2. Search Box Implementation

*   Inside the `.card`, a `div` with class `search` is created.
*   It contains an `input` field of `type="text"` with a `placeholder="Enter city name"` and `spellcheck="false"`.
*   A `button` element with an `img` tag for the search icon (`Images/search.PNG`) is added next to the input field.

### 3. Displaying Weather Details

*   After the search box, a `div` with class `weather` is added to display the weather information.
*   Initially, it includes a placeholder weather icon (`Images/rain.PNG`) with class `weather-icon`, temperature in an `h1` tag (class `temp`, e.g., "22°C"), and city name in an `h2` tag (class `city`, e.g., "New York").
*   Below the city name, another `div` with class `details` is used for humidity and wind speed.
*   Inside `details`, two columns (`div.col`) are created: one for humidity and one for wind speed, each containing an image (e.g., `humidity.PNG`, `wind.PNG`) and relevant text (e.g., "50%", "15 km/h").

### 4. Styling with CSS

*   **Global Styles**: Basic `margin`, `padding`, `font-family`, and `box-sizing` are applied.
*   **Body Background**: A dark background color is set for the `body`.
*   **Card Styling**: The `.card` is styled with a `max-width`, `width`, `linear-gradient` background, `white` text color, `margin: 100px auto`, `border-radius`, `padding`, and `text-align: center`.
*   **Search Bar Styling**: The `.search` div uses `display: flex`, `align-items: center`, and `justify-content: space-between` to align the input and button horizontally.
*   **Input Field and Button**: Styles are applied to remove borders and outlines, set background and text colors, add padding, height, and border-radius. The search button is made circular with `border-radius: 50%` and a `cursor: pointer`. The search icon within the button is sized to `16px` width.
*   **Weather Details Styling**:
    *   The `.weather-icon` is sized to `170px` width with a `margin-top`.
    *   `h1` (temperature) and `h2` (city name) tags within `.weather` are styled for font size and weight.
    *   The `.details` container also uses `display: flex`, `align-items: center`, `justify-content: space-between` to align humidity and wind details in two columns.
    *   Individual `.col` items are flex containers, aligning their content (icon and text). Icons (`.col IMG`) are sized to `40px` width with `margin-right`.
    *   Text elements for humidity and wind are styled with appropriate font sizes and `margin-top`.
*   **Hiding Weather and Error by Default**: Initially, the `.weather` and `.error` divs are set to `display: none` in CSS so they are hidden until a search is performed or an error occurs.

### 5. JavaScript Functionality (API Integration)

*   **API Variables**: `const apiKey` stores your OpenWeatherMap API key, and `const apiUrl` holds the base URL for the weather data API, configured to use `metric` units for Celsius.
*   **`checkWeather` Async Function**:
    *   This `async` function takes `city` name as an argument.
    *   It constructs the full API URL using backticks to embed the `city` and `apiKey`.
    *   `fetch` is used to make an asynchronous request to the API.
    *   The `response` is then converted to JSON using `response.json()`.
    *   **Error Handling**: It checks `response.status === 404` to detect an invalid city name.
        *   If `404`, the error message (`.error`) is displayed, and weather details (`.weather`) are hidden.
        *   Otherwise (in the `else` block), the error message is hidden, and weather details are displayed.
*   **Updating UI Elements**:
    *   `document.querySelector()` is used to select HTML elements by their class names (e.g., `.city`, `.temp`, `.humidity`, `.wind`, `.weather-icon`).
    *   `innerHTML` is used to update the city name, temperature (rounded using `Math.round()`), humidity, and wind speed.
    *   Units (°C, %, km/h) are concatenated to the respective values.
*   **Dynamic Weather Icon**:
    *   The `data.weather.main` property from the API response provides the weather condition (e.g., "Clouds", "Clear", "Mist", "Drizzle").
    *   An `if-else if` block checks this condition and updates the `src` attribute of the `.weather-icon` element to display the corresponding image from the `images` folder (e.g., `Images/clouds.PNG`).

### 6. Search Functionality

*   **Element Selection**: Variables `searchBox` and `searchBtn` are created to select the input field and search button respectively.
*   **Event Listener**: An `addEventListener` is attached to the `searchBtn` to listen for `click` events.
*   **Calling `checkWeather`**: When the search button is clicked, the `checkWeather` function is called, passing `searchBox.value` (the city name entered by the user) as an argument.
*   **Initial State**: On page load, the `checkWeather` function is called to display default weather information (e.g., for "Bangalore"), but this is later removed so that the weather information only displays after user input. The weather details are initially hidden by default and only become visible after a successful search.

---
