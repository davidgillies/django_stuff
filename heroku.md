## Heroku Commands

# Databse copy: copy production to stage
heroku pg:backups:restore action-tool-production::b101 DATABASE_URL --app action-tool-stage

