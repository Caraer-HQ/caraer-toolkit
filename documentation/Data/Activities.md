# Activities

An **Activity** records work, communication, or an event connected to the work your team is doing. Activities help people understand what happened, what is happening, and what needs attention next.

Activities can include a title, description, date, body, and status. The exact information depends on the Activity type and workspace configuration.

## Action

The **Action** Trait lets a Record represent an action or interaction.

Examples include:

- a call or meeting;
- a note or follow-up;
- a recorded website interaction;
- a system or follow-up action.

Activity, Page Visit, Web Event, and Web Session are examples of Objects that can use Action behaviour.

## Message

The **Message** Trait lets a Record represent a message or other communication.

It may include:

- sender and recipients;
- message content;
- channel;
- delivery status;
- conversation or thread information.

For example, a WhatsApp message may be related to the people or company involved using Relations such as **sent to**, **received from**, or **about**.

## Event

The **Event** Trait lets a Record represent a scheduled or time-based event.

It may include:

- start and end time;
- timezone;
- attendees;
- location;
- reminders;
- event status.

Examples include meetings, appointments, and scheduled follow-ups.

## Task

The **Task** Trait lets a Record represent work that needs to be completed.

It may include:

- status;
- start date and due date;
- priority;
- owner or assignee;
- estimate;
- completion information;
- project or calendar connection where enabled.

For example, an Onboarding Record can use Task behaviour while remaining an Onboarding Record. It does not become a separate Task Record.

## Follow-up Activities

Activities can be connected in a sequence, such as an introductory meeting followed by a proposal review or a customer call followed by a Task to send a proposal.

```text
Activity: Introductory meeting
└── Follow-up Activity: Proposal review
    └── Task: Send proposal
```

## Activities and Relations

An Activity describes something that happened or needs to happen. A Relation connects the Activity to independently existing Records, such as a Company, Candidate, Employee, or Project.

## Access

Activity types, fields, calendar connections, and visibility may require administrator access. If an Activity type is missing or cannot be changed, contact your Caraer administrator or representative.
