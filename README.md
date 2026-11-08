# Automated Travel Booking Processing System

An automated booking request management system built with **n8n**. It receives booking requests through a webhook, validates the destination, and routes requests to dedicated flight or hotel processing workflows.

The system uses Google Sheets for record keeping and Gmail for notifications.

## Overview

The main workflow accepts `POST` requests through:

```text
/webhook/api-gateway
```

The exact production URL depends on your n8n instance.

### Supported Booking Types

| Booking Type | Sub-workflow | Current Function |
|---|---|---|
| `flight` | Flight Booking Processing | Checks destination against a predefined list |
| `hotel` | Hotel Processing | Records booking details and sends an email notification |

## Architecture

```text
             Incoming Request
                    |
                    v
               API Gateway
                    |
                    v
             Validate Destination
                    |
                    v
              Route Booking
                /       \
               /         \
            Flight       Hotel
              |            |
              v            v
        Flight Handler  Hotel Handler
              |            |
              v            v
        Destination     Format Booking
          Check             Details
              |            |
              v            v
        Google Sheets  Gmail Notification
              |
              v
        Review Notification
        (if unsupported)

          Central Error Handler
```

## Main Workflow

The main booking workflow handles:

1. Receiving booking requests through a webhook.
2. Checking whether a destination was provided.
3. Routing requests based on `bookingType`.
4. Sending flight requests to the flight sub-workflow.
5. Sending hotel requests to the hotel sub-workflow.
6. Sending email notifications for invalid requests.
7. Logging invalid booking requests in Google Sheets.

## Request Format

Example flight booking request:

```json
{
  "name": "John Doe",
  "bookingType": "flight",
  "destination": "Nigeria"
}
```

Example hotel booking request:

```json
{
  "name": "John Doe",
  "bookingType": "hotel",
  "destination": "Ghana"
}
```

Supported booking types:

```text
flight
hotel
```

## Flight Booking Processing

The flight sub-workflow receives:

- `name`
- `bookingType`
- `destination`

It performs the following operations:

1. Sends an HTTP GET request to JSONPlaceholder.
2. Checks the destination using JavaScript.
3. Compares the destination against a predefined list.
4. Marks supported destinations as approved.
5. Sends unsupported destinations for manual review.
6. Logs booking information in Google Sheets.

### Important: Destination Validation

The current destination approval logic uses a predefined JavaScript list:

```javascript
const supportedDestinations = [
  "nigeria",
  "ghana",
  "kenya"
];
```

**The JSONPlaceholder API response is not used to determine destination availability or approve bookings.**

Destination approval is based entirely on the predefined JavaScript list.

The JSONPlaceholder request is currently a demonstration API request, not a real flight booking or availability integration.

## Hotel Booking Processing

The hotel sub-workflow:

1. Receives booking information.
2. Formats the booking details.
3. Adds a booking status.
4. Generates a timestamp.
5. Sends an email notification through Gmail.
6. Records the booking in Google Sheets.

The current workflow uses the status:

```text
Hotel booking received
```

**Note:** The workflow does not connect to a real hotel reservation platform or confirm an actual hotel reservation.

## Error Handling

The project includes a centralized error handler.

It uses an n8n Error Trigger to detect workflow failures and sends an email containing:

- Workflow name
- Execution ID
- Error message

This helps identify and investigate failed automation executions.

## Technologies Used

- n8n
- Webhooks
- JavaScript
- HTTP Request
- Google Sheets
- Gmail

## Setup

1. Create an n8n instance.
2. Import the workflow JSON files.
3. Configure Google Sheets credentials.
4. Configure Gmail credentials.
5. Select the appropriate spreadsheets and worksheets.
6. Confirm the sub-workflow connections.
7. Test flight and hotel booking requests.
8. Test invalid destination handling.
9. Test the error handler.
10. Activate the workflows after successful testing.

The supplied exports show the main booking workflow and the flight and hotel sub-workflows as inactive. The error handler is active.

## Repository Contents

| File | Description |
|---|---|
| `Booking processsing.json` | Main booking gateway |
| `Flight booking processing.json` | Flight request processing |
| `Hotel sub workflow.json` | Hotel request processing |
| `My workflow.json` | Central error handler |

## Current Scope and Limitations

This project represents an initial implementation of a booking automation workflow.

Current limitations:

- No real flight booking API is integrated.
- No real hotel reservation API is integrated.
- JSONPlaceholder is used as a demonstration endpoint.
- Destination approval relies on a predefined JavaScript list.
- Flight booking availability is not verified.
- Hotel reservations are not confirmed with a hotel provider.
- Workflows require activation and end-to-end testing.

## Future Improvements

- Integrate a real flight booking API.
- Integrate a hotel reservation API.
- Implement real-time availability checks.
- Add booking confirmation and reference numbers.
- Improve validation and error handling.
- Add customer-facing booking responses.

---

**Project Status:** Initial Implementation  
**Workflow Platform:** n8n
<img width="1758" height="771" alt="Flight booking processing" src="https://github.com/user-attachments/assets/3ddab936-148c-44b4-a8fc-57943ed98850" />
<img width="1652" height="818" alt="Booking processing" src="https://github.com/user-attachments/assets/740eec47-b8a1-4f60-8d21-dd1618b82989" />
<img width="1153" height="371" alt="Booking Sheet" src="https://github.com/user-attachments/assets/3ed1c687-74f3-4f2f-9948-e8dc17cf11db" />

