+++
title = "Get Started"
updated = 2026-01-21
authors = ["Violet Chan"]
+++

# Welcome!

Volery is currently in the early stages of development! There are currently no demoes or complete versions to try out, but, you can always check out the latest work on the Github repositories! 

Volery is split into two parts, [the server](https://github.com/OSF-PDX/Volery-server) and [the client](https://github.com/OSF-PDX/volery-client). You can download and try out the client, instructions are provided below, but check the repository for the most up to date directions.


# The client
Our client is written using the Expo React Framework and uses WatermelonDB for local caching in the mobile app version. Currently, the front-end supports android and web. We use the Android Studio android phone emulator for our testing.

## Running the client
1. download the [client repository](https://github.com/OSF-PDX/volery-client)
2. make sure you have `npm` installed
3. In the command line, navigate to the `expo-frontend` directory and run `npm install` to make sure all packages are installed, then run `npx  expo run` to build and emulate the app.
4. when the front-end starts it will try to connect to the server on `localhost:3000` if it's unable to connect it  will not  crash, it will simply do its fallback behavior.

# The server
Our server is written in the Express framework and uses a Postgres database management system. Our current plan is to sync the Volery database with any backend a conference organizer is already using via an abstract interface to which a plug-in for any CRM or other data management system can be written. We are currently working on SalesForce support.

