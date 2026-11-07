# Automated Travel Booking Processing System

An n8n-based workflow automation system designed to process travel booking requests, validate submitted information, check flight and hotel availability, and manage booking notifications.

## Project Overview

This project automates the initial stages of travel booking processing by connecting multiple services through n8n workflows.

It reduces manual processing, improves request validation, and organizes booking information.

## Workflow Architecture

The system follows this general process:

1. **Webhook Trigger:** Receives incoming travel booking requests.
2. **Data Validation:** Checks submitted booking information.
3. **Flight Processing:** Routes flight requests to the appropriate sub-workflow.
4. **Hotel Processing:** Routes hotel requests to the appropriate sub-workflow.
5. **API Integration:** Communicates with external REST APIs for availability checks.
6. **Notifications:** Sends booking-related email notifications through Gmail.
7. **Data Storage:** Records booking information in Google Sheets.

## Technologies Used

- n8n
- Webhooks
- REST APIs
- JSON
- Gmail
- Google Sheets
- Workflow Automation

## Key Features

- Automated booking request processing.
- Input validation.
- Modular sub-workflow architecture.
- Flight and hotel request handling.
- API integration.
- Automated email notifications.
- Booking data management.

## Repository Contents

- `automated-travel-booking-system.json` – Exported n8n workflow configuration.

## Setup

1. Install or access an n8n instance.
2. Import the workflow JSON file.
3. Configure the required credentials and integrations.
4. Configure the external API endpoints.
5. Activate the workflow.
6. Submit a booking request through the configured webhook.

**Note:** API credentials and service configurations must be supplied separately. They are not included in the exported workflow.

## Project Purpose

Built as a practical demonstration of workflow automation, API integration, webhook processing, and modular system design.
