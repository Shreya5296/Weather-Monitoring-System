# Weather-Monitoring-System
To make this happen we need to do a lot of things on our end- 
1. Write a program on Arduino IDE to get value from sensors
2. Set up “No SQL database” using Google Firestore
3. Create an HTML page to display the sensor’s value
4. Set up
5. Set up a web server using flask.

So, Let’s set up the database first and then we will get the value from ESP32.
1. Click on Sign in.
2. After Sign up, Click on Go to Console.
3. Select the “Add project” option to create a new project.
4. Enter your project name, give the project a suitable name and then click the blue Continue button.
5. After that click on the Continue button again.
6. Disable the “Enable Google Analytics” option for this project as it will not be needed.
7. Finally, select Add Firebase.
8. Firebase will begin to set up the project. Once completed select Continue.
9. Click “Settings Symbol” next to Project Overview.
10. Select “Service Accounts” and the select “Python” and then click on “Generate new private key”.
11. Go to Downloads and save this file
12. Click on “Firestore Database”
13. Select “Create database”
14. Select “Sart in test mode”, Click on “Next”.
15. Select “Asia” under Cloud Firestore location. You can choose any location. Click on “Enable”.
16. Click on “+Start collection”.
17. Write the “Collection ID” data.
18. Click on “Next”
19. Write the DocumentID data and insert the default values of temperature, humidity, pressure, altitude, and time.
20. As per input add data types too. For a time it would be a timestamp and for others, it would be numerical. Enter default values in field.
21. So our firestore database is set now. To insert the values in the database, we need to call an API. But before that we must get values from sensors.

The next task is to get the values from the ESP32 board.
Step -1: Gather the following devices from your IoT kit:
● 1 x ESP32
● 1 x USB Cable
● 1 x Breadboard
● 9 x Jumper wires
● 1 x DHT11 sensor
● 1 x BMP180 sensor

Step -2: Let’s do connections:
● Supply VCC(positive) from ESP32 (VIN PIN) to the breadboard positive rail.
● Supply GND(negative) from ESP32 (GND PIN) to breadboard negative rail. 

Connect BMP180 sensor
● Connect VCC of BMP180 with the positive rail of the breadboard.
● Connect GND of BMP180 with the negative rail of the breadboard.
● Connect SCL pin with ESP32 pin 22.
● Connect SDA pin with ESP32 pin 21. 

Connect DHT11 sensor
● Connect VCC of DHT11 with the positive rail of the breadboard
● Connect GNDf DHT11 with negative rail of the breadboard

Step -3: Write program on Arduino IDE to get value from sensors

Output:
Compile and upload the program to ESP32 board using Arduino IDE
● Verify the program by clicking the Tick option
● Upload the program by clicking the arrow option
● Connect Data/Outpin pin with ESP32 pin 19

Step -4: Set up a Flask server and create an API to fetch data from Database. Later, we will display these data on an HTML webpage using the post method.
1. Design the html page using bootstrap to make it responsive
2. Set up the server and fetch the real-time values through API.

We need to install Flask on our system if it’s not installed in the system
To avoid conflicts with libraries, install Flask in a virtual environment.
To create and activate a virtual environment, we can simply run the following commands -

Mac/Ubuntu -
python -m venv venv
source venv/bin/activate

Windows -
python -m venv venv
venv\Scripts\activate.bat

Next, we will run the following command to install flask into our virtual environment
pip install flask
Next, we will run the following command to install firebase_admin into our virtual environment
pip install firebase_admin

The flask framework looks for HTML templates in a folder called templates. So, folder called “templates” contain HTML page there. Here is how the web app directory tree should be like at this point:
Python or .py script stays outside of the templates folder. So first will start working on our main.py file
Also, to start the application, we would call the main function
● Add google firestore credentials
● Store firestore credentials in variable cred
● credentials.Certificate function is used for authentication with google firebase
● Call the add data API ans using POST method display on HTML page

Let’s make function add_data()
● Make variable to save values fo temperature, humidity, pressure and altitude.
● request.json.get() method is used to request the value from firebase in json format
● Add all values in one string
● If get the values print success otherwise in exception through error

Next, we are creating a function “index” that returns the (home.html) i.e. our webpage The function is mapped to the home using '/' URL. 
This means when the user navigates to “host:5000”, the home function will run and the output will be displayed on the webpage.
Using the “render_template” method from the flask framework, we passed an HTML file to the method and it returned to the browser when the user visits the “URL” associated with that template.
Save the data as per latest time using order.by function
However, here we need to write the IP address of the system instead of the local host, as we are dealing with two systems, ESP32 and your computer. So, we send requests to the computer by using its IP address.
Open Command prompt and then type ipconfig
Now open the Arduino program, which we have written in the last class, Now we will add some HTTP requests
Write the IP address of your computer To find IP address, Go to command prompt/Terminal
Write ipconfig
Add http object for HTTPClient
Start the HTTP server using http begin()

Output:
Compile and upload the program to ESP32 board using Arduino IDE
● Verify the program by clicking the Tick option
● Upload the program by clicking the arrow option
● Run the Program
Open the Google firebase too in another window.
Now run the main.py to run the flask server
If get error while running the program then follow the below procedure
Go to the folder directory and then run the below command

Windows
python -m venv venv
venv\Scripts\activate.bat
pip install flask
pip install firebase_admin
python main.py

Mac/Ubuntu -
python -m venv venv
source venv/bin/activate
pip install flask
pip install firebase_admin
python main.py

● Copy the http://192.168.0.104:5000/ and paste on the browser and click the enter button.
● Output window will be shown








