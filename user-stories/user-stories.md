# Airbnb Clone User Stories

## Overview
This document contains user stories derived from the use case diagram created in Task 1. These stories describe the interactions between actors (Guest, Host, Admin) and the Airbnb Clone system, focusing on core functionalities.

## User Stories
1. **As a Guest, I want to register an account so that I can book properties and manage my bookings.**
   - Acceptance Criteria:
     - I can provide an email and password to register.
     - I receive a confirmation email.
     - I can log in after registration.

2. **As a Host, I want to add a property so that I can list it for guests to rent.**
   - Acceptance Criteria:
     - I can enter property details (name, description, location, price).
     - The property is submitted for admin approval.
     - I receive a notification when approved.

3. **As a Guest, I want to create a booking so that I can reserve a property for my stay.**
   - Acceptance Criteria:
     - I can select a property and choose dates.
     - The system checks availability and calculates the total price.
     - I receive a confirmation after booking.

4. **As a Host, I want to process a payout so that I can receive payment for my bookings.**
   - Acceptance Criteria:
     - I can request a payout after a booking is completed.
     - The system records the transaction and transfers funds.
     - I receive a confirmation of the payout.

5. **As an Admin, I want to approve properties so that only valid listings are available to guests.**
   - Acceptance Criteria:
     - I can view pending property submissions.
     - I can approve or reject properties with a reason.
     - Approved properties are visible to guests.

## Notes
- These stories are based on the use case diagram in `use-case-diagram/airbnb-clone-use-case.png`.
- Additional stories can be added for secondary use cases (e.g., "Send Message", "View Analytics") as needed.