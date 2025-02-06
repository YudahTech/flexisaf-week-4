Weather App

Description

The Weather App is a simple web application that allows users to search for a city and retrieve the weather forecast for that location. The application fetches real-time weather data from an API and displays relevant information such as temperature, humidity, and weather conditions.

Learning Outcomes

This project covers the following key concepts:

1. Fetching Data from an API

Uses the fetch API to request data from a weather API.

Parses the response and updates the UI accordingly.

Relevant Command:

useEffect(() => {
    const fetchForecast = async () => {
      try {
        const res = await fetch(
          `https://api.openweathermap.org/data/2.5/forecast?q=${city}&units=metric&appid=${apiKey}`
        );
        const data = await res.json();
        if (data.cod !== "200") {
          alert("City not found");
          throw new Error("City not found");
        }
        console.log(data);
        console.log(data.list);
        setForecast(groupByDay(data.list));
        setShowWeather(true);
        setError("");
      } catch (err) {
        setShowWeather(false);
        setError(err.message);
      }
    };

    fetchForecast();
  }, [city, apiKey]);
  
2. Handling User Input

Captures user input from the search box.

Dynamically updates the UI based on user input.

Relevant Command:

  const cityInputRef = useRef(null); // Reference for the input box
  const [city, setCity] = useState("Abuja"); // Default city

const handleSearch = () => {
    const inputCity = cityInputRef.current.value; // Get value from input
    if (inputCity) {
      setCity(inputCity); // Update the city and trigger re-fetch
    } else {
      alert("Please enter a valid city name.");
    }
  };

  <div className={styles.inputWrapper}>
          <input
            type="text"
            placeholder="Find your location..."
            ref={cityInputRef}
          />
          <button onClick={handleSearch}>Find</button>
        </div>


3. Error Handling

Implements error handling to manage incorrect city names or network failures.

Relevant Command:

catch (err) {
        setShowWeather(false);
        setError(err.message);
      }
      I also added this:
      if (data.cod !== "200") {
          alert("City not found");
          throw new Error("City not found");
        }
        because fetch API doesn't identify some of those errors as actual errors.



Usage Guide

Enter a city name in the search box.

Click the "Search" button.

The weather information will be displayed.

If an invalid city is entered, an error message will appear.

Example

Try searching for: Lagos, New York, or Tokyo.





# React + Vite

This template provides a minimal setup to get React working in Vite with HMR and some ESLint rules.

Currently, two official plugins are available:

- [@vitejs/plugin-react](https://github.com/vitejs/vite-plugin-react/blob/main/packages/plugin-react/README.md) uses [Babel](https://babeljs.io/) for Fast Refresh
- [@vitejs/plugin-react-swc](https://github.com/vitejs/vite-plugin-react-swc) uses [SWC](https://swc.rs/) for Fast Refresh
