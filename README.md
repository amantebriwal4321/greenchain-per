# greenchain-per
Backend API for GreenChain Food Waste Tracking System
## Overview

This is the backend API for the GreenChain Food Waste Tracking System. It provides endpoints to record and retrieve food waste data, enabling tracking and analysis for sustainability and waste reduction efforts.

## Features

- RESTful API for saving and querying waste records
- Mongoose (MongoDB) data storage
- Supports different waste types (plastic, paper, metal, glass, organic, electronic, other)
- Quantity and weight recording
- Includes metadata: deviceId, date, location, notes

## Getting Started

### Prerequisites

- Node.js (v14+ recommended)
- MongoDB Database (local or remote)

### Installation

1. Install dependencies:
    ```bash
    cd backend
    npm install
    ```

2. Create a `.env` file at the root of the `backend` folder (optional) and set your MongoDB URI:
    ```env
    MONGO_URI=mongodb://localhost:27017/greenchain
    ```

3. Start the server:
    ```bash
    npm start
    ```

The server defaults to port 3000 unless otherwise specified.

### API Endpoints

#### POST `/api/waste`

Save a new waste record.

- **Request Body (JSON):**
  ```json
  {
    "deviceId": "your-device-id",
    "weightKg": 1.2
  }
  ```
  - `deviceId` (string, required)
  - `weightKg` (number, required, kg unit; used for both `quantity` and `weightKg` in the model)

- **Response:**
  - `201 Created` with the saved record
  - `400` for missing or invalid fields

#### GET `/api/waste`

Fetch all recorded waste data, sorted with most recent first.

- **Response:**
  - JSON array of waste records

### Waste Record Model

Each waste record stores:

- `deviceId`: String, device identifier
- `type`: String, waste type (`plastic`, `paper`, `metal`, etc.), default `"other"`
- `quantity`: Number, amount of waste (usually matches `weightKg`)
- `weightKg`: Number, waste weight in kilograms
- `unit`: String, measurement unit (`kg`, `g`, `pieces`, `liters`)
- `date`: Date, when the waste was recorded
- `location`: String (optional)
- `notes`: String (optional)

### Example Data

```json
{
  "deviceId": "scale-01",
  "type": "other",
  "quantity": 2.5,
  "weightKg": 2.5,
  "unit": "kg",
  "date": "2024-05-04T13:45:00Z"
}
```

## Development

Routes are defined in `backend/routes/wasteRoutes.js`. The MongoDB model is in `backend/models/WasteRecord.js`. Database configuration is set in `backend/config/db.js`.

## License

[ISC](LICENSE)

## Author
Aman Tebriwal
GreenChain Team


