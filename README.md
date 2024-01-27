# Image Rectangle Extractor Microservice

This microservice extracts coordinates of black rectangles from PNG images. It is designed to receive PNG files and return a list of rectangles with unique IDs and coordinates of their four vertices.

## Table of Contents

- [Introduction](#introduction)
- [Features](#features)
- [Getting Started](#getting-started)
- [Prerequisites](#prerequisites)
- [Installation](#installation)
- [Usage](#usage)
- [Dockerization](#dockerization)
- [API Endpoint](#api-endpoint)
- [File Structure](#file-structure)
- [Dependencies](#dependencies)


## Introduction

This microservice is built to process PNG images containing black rectangles. It identifies these rectangles and provides their coordinates as JSON objects.

## Features

- Accepts PNG files with black rectangles.
- Extracts coordinates of black rectangles.
- Returns a list of JSON objects with unique IDs and rectangle coordinates.

## Getting Started

### Prerequisites

Ensure you have Node.js and npm installed on your machine.

### Installation

1. Unzip the repository:


2. Install dependencies:

    ```bash
    cd enurgen
    npm install
    ```

### Usage

1. Run the microservice:

    ```bash
    npm start
    ```

2. Send a POST request with a PNG file to `http://localhost:3000/extract-rect-coords`.

### Dockerization

Create a Dockerfile in the same directory as app.js:

  ```bash
    FROM node:14
    WORKDIR /app
    COPY package.json package-lock.json ./
    RUN npm install
    COPY . .
    EXPOSE 3000
    CMD ["node", "app.js"]
  ```

**Build the Docker image:**  


 ```bash
      docker build -t rect-coords-microservice .
  ```

**Run the Docker container:**


  ```bash
  docker run -p 3000:3000 rect-coords-microservice
  ```

### API Endpoint

- **POST /extract-rect-coords:** Accepts PNG files, processes them, and returns a JSON array of rectangles.

```bash

curl --location 'http://localhost:3000/extract-rect-coords' \
--form '=@"/public/images/simple.png"'

```
<img width="870" alt="Screenshot 2024-01-27 at 5 50 46 AM" src="https://github.com/ashmitaggarwal/enurgen-api/assets/26399866/8af26aea-d93b-4c6a-8f01-ab945e20d864">

Resppnse

```bash

{
    "rectangles": [
        {
            "id": "5d5754fe-4998-4636-af0e-124f14fe3426",
            "coordinates": [
                75,
                56,
                124,
                455,
                124,
                455,
                75,
                455
            ]
        },
        {
            "id": "2813d1cb-a72d-4d85-bc1b-0f929090d299",
            "coordinates": [
                231,
                56,
                280,
                455,
                280,
                455,
                231,
                455
            ]
        },
        {
            "id": "94f34431-7011-4438-bf26-825afe76c165",
            "coordinates": [
                387,
                56,
                436,
                455,
                436,
                455,
                387,
                455
            ]
        },
        {
            "id": "9db17bc3-ae20-4bba-98c0-0d2fd4a47187",
            "coordinates": [
                75,
                57,
                124,
                455,
                124,
                455,
                75,
                455
            ]
        }
    ],
    "status": 200
}

```

### File Structure

- **app.js:** Main entry point for the microservice.
- **utils.js:** Contains utility functions for rectangle extraction.

### Dependencies

- Express.js
- express-fileupload
- pngjs


