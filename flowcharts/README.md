# Airbnb Clone Data Flow Diagram

## Overview
This directory contains a Data Flow Diagram (DFD) that maps the data flow within the Airbnb Clone system. The diagram, created using Draw.io, illustrates how data moves between external entities, processes, and data stores for core backend operations.

## Components
### External Entities
- Guest
- Host
- Admin
- Payment Gateway

### Processes
- Authenticate User
- Manage Property Listings
- Process Booking
- Handle Payment
- Send Notifications

### Data Stores
- User Database
- Property Database
- Booking Database
- Payment Database

### Data Flows
- Guest → Authenticate User → User Database
- Host → Manage Property Listings → Property Database
- Guest → Process Booking → Booking Database
- Guest → Handle Payment → Payment Database → Payment Gateway
- Process Booking → Send Notifications → Guest/Host
- Admin → Manage Property Listings

## Diagram
- File: `data-flow.png`
- Description: A visual representation of data inputs, processes, and outputs within the system.

## Usage
- Review the PNG file to understand data movement.
- Use this diagram to design backend workflows and database interactions.

## Notes
- The DFD is based on the features from `features-and-functionalities/`.
- The current date is July 01, 2025, and the diagram reflects real-world data flow needs.