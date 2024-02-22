# ssgtm-event-userproperty
Current PoC of Reverse Engineering GA4 data collection and processing

# Motivation
Unfortunately User Properties feature in GA4 is a blackbox, they are not reflected in each and every event in the BigQuery.
For example:
If you set the User Property for a user in iOS.
It won't reflect in the user events happening via Web / Measurement Protocol (with the same user-id), it will only aggregate in the BigQuery Users Export.

And the BigQuery Users Export is a snapshot of the users that interacted with you that day, not every user that has interacted with your business ever since.

# Solution

<img width="1077" alt="Captura de Tela 2024-02-22 às 19 34 26" src="https://github.com/leodantas-381/ssgtm-event-userproperty/assets/70772539/93f21e19-239c-46c0-ac7b-8ccf4e465b7e">

We have users collection and each document is a user.
Each user can have multiple user properties (up map).

There is an event to set_user_properties, which creates/updates the user properties.

Each and every other event will fetch the user properties key-values and store it together with the event, event_parameters and every other information you like.
This way, if user_id 123456 is set user_property "user_status"="cancelled", it will reflect in each and every event of this user_id, no matter the platform.

# Status
Work in Progress
Currently using the GA4 Web event only, and its client-id as identification.

Features Roadmap
- User-id support
- Storing in the client the user document id

