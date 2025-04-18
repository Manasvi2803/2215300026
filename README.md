# Average Calculator HTTP Microservice

A RESTful microservice that calculates averages for different types of numbers (prime, Fibonacci, even, random) while maintaining a sliding window of unique values.

## Features

- REST API endpoint at `/numbers/{numberid}` with support for different number types:
  - `p`: Prime numbers
  - `f`: Fibonacci numbers
  - `e`: Even numbers
  - `r`: Random numbers
- Configurable sliding window mechanism (default size: 10)
- Third-party API integration for fetching numbers
- Unique number storage with oldest-replacement strategy
- Timeout handling (500ms limit)
- Formatted responses with before/after states and calculated averages

## API Endpoints

### GET /numbers/:numberId

Fetches a new number of the specified type from an external service, stores it, and returns the before/after state along with the average.

**Parameters:**
- `numberId`: One of `p` (prime), `f` (fibonacci), `e` (even), or `r` (random)

**Response:**
```json
{
  "before": [1, 2, 3],           // Numbers before the new addition
  "after": [1, 2, 3, 5],         // Numbers after the new addition
  "average": 2.75,               // Average of numbers in the window
  "responseTime": "123ms"        // Time taken to process the request
}
```

### GET /health

Health check endpoint to verify service status.

**Response:**
```json
{
  "status": "UP",
  "message": "Service is healthy"
}
```

## Running the Service

```bash
# Install dependencies
npm install

# Start the service
npm run dev
```

## Implementation Details

- **Window Size**: Fixed at 10 numbers per type
- **Uniqueness**: Duplicate numbers are automatically discarded
- **Error Handling**: Responses taking longer than 500ms or encountering errors are ignored
- **Storage Strategy**: When the window size is reached, the oldest number is replaced with the newest
