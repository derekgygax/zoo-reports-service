
# VENV
## Make a .venv for the project and run it (does NOT go to git)
directly done in VS code
  mac: cmd shift p
    type Python: Create Environment
    choose venv
OR
python3 -m venv .venv
source .venv/bin/activate

## Install what is needed in the venv
pip install fastapi "uvicorn[standard]"

## Lock the necessary things in a requirements.txt file
pip freeze > requirements.txt



# START PROJECT
## location
Top level
	main.py is where everything starts

## start the app and reload on changes. main is module, app is instance. in main.py
uvicorn main:app --reload

# DOCS by default for API
## /docs gives you an interactive documentation on your API. You can even click "try it out" for each endpoint
http://localhost:8000/docs

## /redoc gives you an API documentation. NOT interactive
http://localhost:8000/redoc

# Load ENV variables
## Add load_dotenv() in the following files
database.py
  load_dotenv()
main.py
  load_dotenv()
alembic/env.py
  load_dotenv(dotenv_path=os.path.join(os.path.dirname(__file__), '..', '.env'))
security.py
  load_dotenv()

# Alembic

## Start using alembic
alembic init alembic

## Add DB models to alembic/env.py
You MUST define the DB models at the top of main.py

## Timezones in DB
###  TODO FOR RETRIEVING THE TIMEZONE!!
### Assuming `created_at` is a timezone-aware datetime in UTC
### user_timezone = pytz.timezone("America/New_York")  # Example user timezone
### local_time = post.created_at.astimezone(user_timezone)
### print(local_time)  # This will display the time converted to the user's timezone

## DB migrations Alembic
### generate a migration - after you have changed your models
alembic revision --autogenerate -m "Describe the migration here"

### apply migrations
alembic upgrade head

# Define DB models in main.py
You MUST define the DB models at the top of main.py for anything to run
