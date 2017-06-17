Title: Database initialization on Heroku 
Date: 2017-06-03
Author: Bambridge E. Peterson

500: Internal Server Error is found on my personal webpage when trying to register. I use the

    :::bash
    heroku logs --app appbep

command to see the errors. I get the following output:

    #!python
    ProgrammingError: column user.member_since does not exist

Basically there appears to be a discrepancy between the current version of my database and the code I'm using. I have a local development environment, staging-environment and the production environment, and I must admit I haven't yet automated the migration and update phase of database deployment. Basically I had run 

    :::python
    db.drop_all()

from a shell and then 

    :::python
    db.create_all()

to re-initialize the database. Clearly this won't work if I already have data in the database - currently, there was nothing of importance stored there yet. After performing those operations, I had to log in via the command line to access my *postgres* database using the 

    :::bash
    heroku pg:psql

command. It was there I had to delete the latest version stored in the *alembic_version* table. After that, I deleted the migrations folder, reran the db inititialzation command, committed an initial migration and upgraded to that version of the database.  I really need to work on the deployment process of my application, particularly the database deployment aspects.
    


