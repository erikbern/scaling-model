# Modal Price Estimator

An interactive price calculator for Modal applications that simulates container scaling behavior and estimates costs based on queuing theory.

## Overview

This tool helps you understand and estimate the cost of running applications on Modal by modeling how containers scale in response to varying request loads. It simulates:

- Container states (busy, cold starting, draining/idle)
- Request queuing and processing
- Cold start delays
- Container keepalive behavior
- Cost estimation based on container usage

## Running the Application

Serve the files using a local HTTP server:

```bash
python -m http.server 8000

Then navigate to `http://localhost:8000` in your browser.

## Features

### Interactive Parameters

- **Requests/min**: Base request rate (1-10k requests per minute)
- **Execution time**: How long each request takes to process (1s - 1 hour)
- **Keepalive time**: How long idle containers remain available (1s - 1 hour)
- **Cold start time**: Container initialization delay (1s - 1 hour)
- **Buffer containers**: Number of extra idle containers to maintain
- **Warm containers**: Minimum number of containers to keep warm
- **Price per hour**: Cost per container-hour (configurable)

### Visualizations

- Stacked area chart showing container counts over time
- Queue time overlay showing average request wait times
- Real-time cost estimation based on container usage
- Utilization rate metrics

### Regenerate

Click the "Regenerate" button to generate new random demand patterns while keeping your parameter settings.

## Technical Details

- Built with vanilla JavaScript (ES6+)
- Visualization powered by D3.js v7 (loaded from CDN)
- No build step or dependencies to install
- Simulates 7 days of serverless workload
- Uses Poisson distribution for request generation
- Implements mean-reverting random walk for realistic demand patterns

## Cost Model

Container cost is calculated based on a configurable price per container-hour (default: $3.95), applied to the total container-minutes across all states (busy, cold starting, and draining). Adjust the price per hour slider to match your Modal application's container specifications.
