# Trading Bot Database (MySQL)

This container provisions a MySQL database for the autonomous trading bot. On startup it:
- Ensures MySQL is running on the configured port
- Creates the database, root/app users, and grants privileges
- Applies startup.sql to create tables, indexes, and seed defaults
- Writes db_visualizer/mysql.env for the lightweight DB viewer

## Quick start
1) Start the container or run startup script:
   ./startup.sh

2) Connect to MySQL:
   $(cat db_connection.txt)

3) Optional: Launch the simple DB viewer:
   cd db_visualizer
   source mysql.env
   npm install
   npm start

## Environment variables
See .env.example for required variables:
- MYSQL_URL
- MYSQL_USER
- MYSQL_PASSWORD
- MYSQL_DB
- MYSQL_PORT

These are also exported for the DB viewer in db_visualizer/mysql.env.

## Schema overview
Tables created by startup.sql:
- users, api_keys
- bot_config
- signals
- trades
- news_items
- logs

All tables have sensible indexes, and the script seeds a default admin user and baseline bot_config entries. The script is idempotent and safe to re-run.

## Notes
- Credentials in .env.example are development defaults; replace in production.
- Do not hard-code secrets in source control.
