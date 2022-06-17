Spectrum has 3 main parts which make up the application

1. Frontend SPA
2. API Server
3. Hyperion - Rendering Server

There are also workers to perform background jobs;

1. Athena - Worker for notifications and general processing
2. Chronos - Worker for cron jobs
3. Hermes - Worker for sending emails
4. Mercury - Worker for reputation
5. Vulcan - Worker for search indexing; syncing with Algolia

A desktop version also exists (built with electron) in `/desktop`.  

Spectrum is an online platform which brings a chat-based communities together.  
Currently in read-only mode, Spectrum is powered by:

1. React - Frontend SPA
2. Express.JS - API Sever
3. GraphQL - API Server
4. Flowtype - For type safety
5. Redis - For background jobs and caching
6. RethinkDB - Database
7. PassportJS - Authentication
