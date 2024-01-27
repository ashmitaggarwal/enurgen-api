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

### File Structure

- **app.js:** Main entry point for the microservice.
- **utils.js:** Contains utility functions for rectangle extraction.

### Dependencies

- Express.js
- express-fileupload
- pngjs


