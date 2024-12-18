# API Sample Test

## Debrief

The biggest practical issue I ran into is that the `lastModifiedDate` logic was
too recent to get any meetings. I hardcoded January 2023 as a rough start date
for testing.

The task requested essentially a duplication of the `processCompanies` and
`processContacts` methods, so I endeavored to do so. However, this architecture
leads to a good deal of duplication. From an ease-of-implementation
perspective, I actually think this is just fine. However, it _also_ leads to
duplication of API requests, which is inefficient, slow, and potentially
costly. It would perhaps be better to get the account's companies, then
associate them with contacts and meetings in one go. Reducing the number of
requests would improve performance significantly.

The queue is a nice feature; for the number of contacts here, perhaps
unnecessary, but a forward-looking usage of the mongo API for increased
traffic.

The project could use a linting configuration to make collaboration on Github
less noisy. Warnings for deprecated packages should also be dealt with.

## Getting Started

This project requires a newer version of Node. Don't forget to install the NPM
packages afterwards.

You should change the name of the `.env.example` file to `.env`.

Run `node app.js` to get things started. Hopefully the project should start
without any errors.

## Explanations

The actual task will be explained separately.

This is a very simple project that pulls data from HubSpot's CRM API. It pulls
and processes company and contact data from HubSpot but does not insert it into
the database.

In HubSpot, contacts can be part of companies. HubSpot calls this relationship
an association. That is, a contact has an association with a company. We make a
separate call when processing contacts to fetch this association data.

The Domain model is a record signifying a HockeyStack customer. You shouldn't
worry about the actual implementation of it. The only important property is the
`hubspot`object in `integrations`. This is how we know which HubSpot
instance to connect to.

The implementation of the server and the `server.js` is not important for
this project.

Every data source in this project was created for test purposes. If any request
takes more than 5 seconds to execute, there is something wrong with the
implementation.
