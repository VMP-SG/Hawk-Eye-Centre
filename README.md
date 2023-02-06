# Hawk-Eye Centre

Hawk-Eye Centre is an **integrated data source** powered by Machine Learning capabilities. Using computer vision models and pipelines from the PeekingDuck library, Hawk-Eye Centre can process large volumes of relevant information like people, furniture and cutlery from video feeds. Interested parties may then utilise this data API to perform higher level analysis and service. 

Hawk-Eye Centre's APIs can be accessed via this [link](https://naiscbackend.vmpsg.xyz).
Our integrated Hawk-Eye Centre Dashboard can be found at this [link](https://naisc.vmpsg.xyz).

## 🛠️ To Run (Docker)

1. Clone the repository recursively
```bash
git clone --recurse-submodules https://github.com/VMP-SG/NAISC-Backend.git
```

2. Run the containers with docker-compose
```bash
docker-compose up
```

Hawk-Eye Centre will be hosted at [http://127.0.0.1:3000](http://127.0.0.1:3000) by default.
The online dashboard will be hosted at [http://127.0.0.1:5173/](http://127.0.0.1:5173/) by default.

## 🛠️ To Run (Without Docker)

1. Download Python at [https://www.python.org/downloads/](https://www.python.org/downloads/)

### For Linux
2. Run the following lines of code
```bash
cd NAISC-Backend/
sudo apt-get install ffmpeg libsm6 libxext6 libgeos-dev -y
python3 -m venv .venv
source .venv/bin/activate
pip install -r requirements.txt
python3 main.py
cd ../
```

### For MacOS
2. Run the following lines of code
```bash
cd NAISC-Backend/
python3 -m venv .venv
source .venv/bin/activate
pip install -r requirements.txt
python3 main.py
cd ../
```

### For Windows
2. Run the following lines of code 
```bash
cd NAISC-Backend/
python -m venv .venv
.venv/Scripts/activate
pip install -r requirements.txt
python main.py
cd ../
```

Hawk-Eye Centre will be hosted at [http://127.0.0.1:3000](http://127.0.0.1:3000) by default.

3. Ensure that the backend server is running before running the data dashboard. To run the data dashboard, install yarn at [https://classic.yarnpkg.com/lang/en/docs/install/](https://classic.yarnpkg.com/lang/en/docs/install/)
   
4. Run the following commands
```bash
cd NAISC-Frontend/
yarn
yarn dev
```

The online dashboard will be hosted at [http://127.0.0.1:5173/](http://127.0.0.1:5173/) by default.

## 🎯 Endpoints

### `GET /startAPI`
Description:
```
Starts API data streams
```
Response Content-Type:
```
text/plain
```
Response:
```
API started!
```

### `GET /stopAPI`
Description:
```
Stops API data streams
```
Response Content-Type:
```
text/plain
```
Response:
```
API stopped!
```

#### `GET /api`
Description:
```
Streams all raw and processed data from Hawk-Eye Centre
```
Response Content-Type:
```
text/event-stream
```

Response (JSON):
```js
{
  "A": {
    "raw_frame": "iVBORw0KGgoAAAANSUhEUgAABDgAAALQCAIAAA",
    "labelled_frame": "iVBORw0KGgoAAAANSUhEUgAABDgAAALQCAIAAA",
    "total_people_count": 0,
    "zone_people_count": [3, 0, 1, 1, 2, 0, 2],
    "zone_mapping": [100, 101, 102, 103, 104, 105, 0]
  },
  "B": {...},
  "C": {...},
  "D": {...}
}
```

#### `GET /video/raw/<zone_id>`
Description:
```
Displays raw live camera feed of specified Hawker Centre Zone
```
URL Parameter(s):

`zone_id`: ID of the Hawker Centre Zone (eg. A)

Response Content-Type:
```
multipart/x-mixed-replace
```

Response:
```
Raw Live Camera Feed
```

#### `GET /video/filter/<zone_id>`
Description:
```
Displays live camera feed of specified Hawker Centre Zone with object detection bounding boxes
```
URL Parameter(s):

`zone_id`: ID of the Hawker Centre Zone (eg. A)

Response Content-Type:
```
multipart/x-mixed-replace
```

Response:
```
Live Camera Feed with Bounding Boxes
```

#### `GET /count/zones`
Description:
```
Streams people count from all Hawker Centre zones
```
Response Content-Type:
```
text/event-stream
```

Response:
```js
{
  "E": 13, 
  "D": 4, 
  "A": 11, 
  "B": 7, 
  "C": 11
}
```

#### `GET /count/zone/<zone_id>`
Description:
```
Streams people count for each table from specified Hawker Centre zone
```
URL Parameter(s):

`zone_id`: ID of the Hawker Centre Zone (eg. A)

Response Content-Type:
```
text/event-stream
```

Response:
```js
[3, 0, 1, 1, 2, 0, 2]
```

#### `GET /count/queues`
Description:
```
Streams people count from all Hawker Centre stall queues
```

Response Content-Type:
```
text/event-stream
```

Response:
```js
{
  "2": 1, 
  "0": 1, 
  "1": 5
}
```

#### `GET /count/queue/<stall_id>`
Description:
```
Streams people count from specified Hawker Centre stall queue
```
URL Parameter(s):

`stall_id`: ID of the Hawker Centre Stall (eg. 0)

Response Content-Type:
```
text/event-stream
```

Response:
```js
0
```

#### `GET /occupancy/tables`
Description:
```
Streams occupancy status of all tables in Hawker Centre
```
Response Content-Type:
```
text/event-stream
```

Response:
```js
{
  "140": false, 
  "141": false, 
  ...
  "122": true
}
```

#### `GET /count/tables`
Description:
```
Streams people count from all Hawker Centre tables
```
Response Content-Type:
```
text/event-stream
```

Response:
```js
{
  "140": 0, 
  "141": 0, 
  ...
  "122": 2
}
```

#### `GET /count/table/<table_id>`
Description:
```
Streams people count from specified Hawker Centre table
```
URL Parameter(s):

`table_id`: ID of the Hawker Centre Table (eg. 140)

Response Content-Type:
```
text/event-stream
```

Response:
```js
0
```

# Hawk-Eye Centre Dashboard

One of the many use cases of Hawk-Eye Centre is an online dashboard providing accurate live information on the crowdedness level in selected hawker centres.

Our integrated dashboard can be found at this [link](https://naisc.vmpsg.xyz).

## ✨ Features

1. **Home Page**
   - Heatmap
   - People Count
   - Zonal Count
   - People Count across the Past Day
2. **Feed Page (Admin)**
   - Raw Live Camera Feed
   - Camera Feed with Bounding Boxes 
3. **Customer Analytics Page**
   - Empty Tables Analytics
   - Popular Stalls
   - Stalls with Shortest Queue
# Credits

### Resources
We used the following resources to aid in the development of our project.
- [PeekingDuck](https://peekingduck.readthedocs.io/en/latest/) for their object detection API

### Contributors
The following members contributed to the success of this project. 

1. [Cai Xinjie Noah](https://www.linkedin.com/in/noah-xinjie-cai/) (Frontend Engineer)
2. [Chay Hui Xiang](https://www.linkedin.com/in/hui-xiang/) (Team Lead, Full-Stack Engineer)
3. [Ian Fong](https://www.linkedin.com/in/ian-fong-45a146265/) (Backend Engineer)
4. [Mao Kaiwen](https://www.linkedin.com/in/mkw68768211/) (Backend & Machine Learning Engineer)
