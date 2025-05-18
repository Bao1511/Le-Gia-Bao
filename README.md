# Virtual GPS Location Tracking with CounterFit & Python



**Learning Objectives:**
* Understand how GPS data is typically transmitted (NMEA sentences).
* Learn to set up and use a virtual IoT sensor.
* Practice reading and decoding serial data in Python.
* Get hands-on experience with a common IoT scenario: location tracking.

---

## 🛠️ How It Works: The Technology Stack

This project combines a few key components to simulate and process GPS data:

1.  **CounterFit (The Virtual IoT Lab Bench):**
    * CounterFit acts as our virtual hardware platform.
    * We configure it to run a **UART GPS Sensor**. This sensor simulates a real GPS module that communicates over a serial connection.
    * CounterFit allows us to feed data into this virtual sensor in various ways (manual Lat/Lon, NMEA sentences, or GPX track files).

    *(Imagine CounterFit as a web interface where you can 'plug in' virtual sensors. For this project, we add a GPS sensor that outputs text data just like a real one would.)*

2.  **`counterfit-shims-serial` (The Bridge):**
    * This Python library allows our Python script to "talk" to the virtual serial port (`/dev/ttyAMA0`) that CounterFit exposes for the UART GPS sensor.

3.  **Python Script (`app.py` - Our IoT Application):**
    * **Connects to CounterFit:** Initializes a connection to the running CounterFit application.
    * **Opens Virtual Serial Port:** Uses `counterfit_shims_serial` to listen to the data stream from the virtual GPS sensor.
    * **Reads NMEA Data:** Continuously reads lines of text data from the sensor. This raw data is typically in NMEA format (e.g., `$GNGGA,...`).
    * **Decodes NMEA Sentences:** Uses the `pynmea2` library to parse these NMEA strings into structured objects, making it easy to access specific information like latitude, longitude, time, altitude, etc.
    * **Displays Information:** Prints the decoded, human-readable GPS information to the console.

4.  **`pynmea2` (The GPS Data Translator):**
    * A powerful Python library that understands the NMEA protocol. It takes raw NMEA sentences and converts them into accessible Python objects.

## ⚙️ Setup and Usage Instructions

Follow these steps to get your virtual GPS tracker up and running:

1.  **Prerequisites:**
    * Python 3.x installed.
    * `pip` (Python package installer).

2.  **Install Necessary Python Packages:**
    Open your terminal or command prompt and run:
    ```bash
    pip install counterfit
    pip install counterfit-shims-serial
    pip install pynmea2
    ```

3.  **Start the CounterFit Web Application:**
    In your terminal, run:
    ```bash
    counterfit
    ```
    This will start the CounterFit web server. Open your web browser and go to `http://127.0.0.1:5000`.

4.  **Create the Virtual GPS Sensor in CounterFit:**
    * In the CounterFit web interface:
        * Go to the "Sensors" pane.
        * Under "Create sensor":
            * Select Sensor type: `UART GPS`.
            * Leave Port: `/dev/ttyAMA0`.
            * Click `Add`.
        * The sensor will appear in the "Sensors" list.

5.  **Configure the GPS Sensor Data Feed in CounterFit:**
    * Select the newly created `UART GPS` sensor.
    * Choose a "Source" for the GPS data:
        * **Lat/Lon:** Manually enter Latitude, Longitude, and Satellites. **Check "Repeat"**.
        * **NMEA:** Paste NMEA sentences (e.g., from `nmeagen.org`). **Check "Repeat"**.
        * **GPX file:** Upload a GPX file. **Check "Repeat"**.
    * Click `Set` after configuring your chosen source.

6.  **Prepare Your Python Script:**
    * Save the Python code (provided in the previous response or your working version) as `app.py` in a local directory.

7.  **Run the Python Script:**
    * Open a **new** terminal window (keep the CounterFit terminal running).
    * Navigate to the directory where you saved `app.py`.
    * Execute the script:
        ```bash
        python app.py
        ```

---

## 📊 Expected Output: What You'll See!

When you run `app.py` after correctly setting up CounterFit and the virtual GPS sensor, your terminal will display a stream of decoded GPS information.

**1. Initial Connection Messages:**
Okay, here's a README.md file structured like a presentation to explain how the virtual GPS location tracking project works, including its setup and expected output.

Markdown

# Virtual GPS Location Tracking with CounterFit & Python

## 🚀 Project Overview

Welcome to the Virtual GPS Location Tracking project! This system demonstrates how to simulate a GPS sensor for IoT development, read its data, and decode it into meaningful geographical information. It's based on the concepts from **Microsoft's IoT-For-Beginners curriculum**, specifically the lesson on location tracking (3-transport/lessons/1-location-tracking).

Instead of requiring physical GPS hardware, we use **CounterFit**, a tool for simulating IoT hardware, and a Python script to interact with our virtual GPS sensor.

**Learning Objectives:**
* Understand how GPS data is typically transmitted (NMEA sentences).
* Learn to set up and use a virtual IoT sensor.
* Practice reading and decoding serial data in Python.
* Get hands-on experience with a common IoT scenario: location tracking.

---

## 🛠️ How It Works: The Technology Stack

This project combines a few key components to simulate and process GPS data:

1.  **CounterFit (The Virtual IoT Lab Bench):**
    * CounterFit acts as our virtual hardware platform.
    * We configure it to run a **UART GPS Sensor**. This sensor simulates a real GPS module that communicates over a serial connection.
    * CounterFit allows us to feed data into this virtual sensor in various ways (manual Lat/Lon, NMEA sentences, or GPX track files).

    *(Imagine CounterFit as a web interface where you can 'plug in' virtual sensors. For this project, we add a GPS sensor that outputs text data just like a real one would.)*

2.  **`counterfit-shims-serial` (The Bridge):**
    * This Python library allows our Python script to "talk" to the virtual serial port (`/dev/ttyAMA0`) that CounterFit exposes for the UART GPS sensor.

3.  **Python Script (`app.py` - Our IoT Application):**
    * **Connects to CounterFit:** Initializes a connection to the running CounterFit application.
    * **Opens Virtual Serial Port:** Uses `counterfit_shims_serial` to listen to the data stream from the virtual GPS sensor.
    * **Reads NMEA Data:** Continuously reads lines of text data from the sensor. This raw data is typically in NMEA format (e.g., `$GNGGA,...`).
    * **Decodes NMEA Sentences:** Uses the `pynmea2` library to parse these NMEA strings into structured objects, making it easy to access specific information like latitude, longitude, time, altitude, etc.
    * **Displays Information:** Prints the decoded, human-readable GPS information to the console.

4.  **`pynmea2` (The GPS Data Translator):**
    * A powerful Python library that understands the NMEA protocol. It takes raw NMEA sentences and converts them into accessible Python objects.

**Flow Diagram:**

[User Configures GPS Data in CounterFit UI (Lat/Lon, NMEA, GPX)]
|
v
[CounterFit Web App] -> [Virtual UART GPS Sensor (on /dev/ttyAMA0)]
|                                     ^
| (Simulated NMEA data stream)        | (Listens via counterfit_shims_serial)
v                                     |
[Python Script (app.py)] -----------------------
|
| (Uses pynmea2 to parse)
v
[Decoded GPS Information (Printed to Console)]


---

## ⚙️ Setup and Usage Instructions

Follow these steps to get your virtual GPS tracker up and running:

1.  **Prerequisites:**
    * Python 3.x installed.
    * `pip` (Python package installer).

2.  **Install Necessary Python Packages:**
    Open your terminal or command prompt and run:
    ```bash
    pip install counterfit
    pip install counterfit-shims-serial
    pip install pynmea2
    ```

3.  **Start the CounterFit Web Application:**
    In your terminal, run:
    ```bash
    counterfit
    ```
    This will start the CounterFit web server. Open your web browser and go to `http://127.0.0.1:5000`.

4.  **Create the Virtual GPS Sensor in CounterFit:**
    * In the CounterFit web interface:
        * Go to the "Sensors" pane.
        * Under "Create sensor":
            * Select Sensor type: `UART GPS`.
            * Leave Port: `/dev/ttyAMA0`.
            * Click `Add`.
        * The sensor will appear in the "Sensors" list.

5.  **Configure the GPS Sensor Data Feed in CounterFit:**
    * Select the newly created `UART GPS` sensor.
    * Choose a "Source" for the GPS data:
        * **Lat/Lon:** Manually enter Latitude, Longitude, and Satellites. **Check "Repeat"**.
        * **NMEA:** Paste NMEA sentences (e.g., from `nmeagen.org`). **Check "Repeat"**.
        * **GPX file:** Upload a GPX file. **Check "Repeat"**.
    * Click `Set` after configuring your chosen source.

6.  **Prepare Your Python Script:**
    * Save the Python code (provided in the previous response or your working version) as `app.py` in a local directory.

7.  **Run the Python Script:**
    * Open a **new** terminal window (keep the CounterFit terminal running).
    * Navigate to the directory where you saved `app.py`.
    * Execute the script:
        ```bash
        python app.py
        ```

---

## 📊 Expected Output: What You'll See!

When you run `app.py` after correctly setting up CounterFit and the virtual GPS sensor, your terminal will display a stream of decoded GPS information.

**1. Initial Connection Messages:**

Successfully connected to virtual GPS sensor on /dev/ttyAMA0
Reading and decoding data from virtual GPS sensor...
**2. Stream of Decoded GPS Data (Example):**

The exact output will depend on the data you configured in CounterFit. Here are a few examples based on typical NMEA sentences:

* **If the sensor sends `$GNGGA` or similar sentences:**
    ```
    Time: 02:06:04.001000, Lat: 47.642311 N, Lon: 122.139029 W, Altitude: 164.7 M
    Time: 02:06:05.001000, Lat: 47.642315 N, Lon: 122.139035 W, Altitude: 165.1 M
    ... (repeats with new data if configured in CounterFit)
    ```

* **If the sensor sends `$GPRMC` sentences (pynmea2 might show more fields):**
    ```
    RMC - Time: 100832.00, Status: A, Lat: 47.642311 N, Lon: 122.139029 W, Speed: 0.5, Date: 2025-05-18
    ...
    ```

* **If a line can't be fully parsed by `pynmea2` or is not a recognized sentence for full detail:**
    ```
    Decoded NMEA: <GNTXT, num_messages=01, message_num01=01, message_type01=01, text='ANTARIS ID some_id_here'>
    Could not parse NMEA sentence: $GPXYZ,invalid,data*AB - Error: Sentence <GPXYZ> not supported
    ```

**3. On Exiting (Ctrl+C):**
Stopping GPS data reading and decoding.
Serial port closed.
