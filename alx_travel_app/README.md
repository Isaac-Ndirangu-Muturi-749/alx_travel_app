# alx_travel_app

To generate a `requirements.txt` file for your Django project, including dependencies that are used for the project
1. **Activate Your Virtual Environment:**
   ```bash
   source venv/bin/activate
   ```


3. **Generate `requirements.txt`:**

   ```bash
   pip freeze > requirements.txt
   ```

This `requirements.txt` file will allow others to set up the same environment using:

```bash
pip install -r requirements.txt
```



# alx_travel_app - Django Project Setup

This is a Django-based web application project called **alx_travel_app**. It includes the necessary configurations for creating an API, integrating Swagger for API documentation, and configuring a MySQL database with environment variable management. This README will guide you through setting up the project, running it, and understanding the steps taken to complete the tasks outlined in the project.

## Project Overview

- **Project Name**: alx_travel_app
- **App Name**: listings
- **Dependencies**: Django, djangorestframework, django-cors-headers, celery, rabbitmq, drf-yasg (Swagger)
- **Database**: MySQL
- **API Documentation**: Swagger (using drf-yasg)

## Features

1. **Django Project Setup**:
   - A new Django project named `alx_travel_app` is created.
   - A Django app named `listings` is added to the project.

2. **Database Configuration**:
   - MySQL is configured as the database.
   - Sensitive information such as database credentials is handled using environment variables with `django-environ`.

3. **API with Django REST Framework**:
   - REST API setup for the application.
   - `djangorestframework` is used for API functionality.

4. **CORS Configuration**:
   - CORS headers are configured using `django-cors-headers` to allow cross-origin requests.

5. **Swagger API Documentation**:
   - The project integrates `drf-yasg` to generate interactive Swagger API documentation.
   - The documentation is accessible at `/swagger/`.

6. **Celery & RabbitMQ**:
   - Celery is used for asynchronous task management, with RabbitMQ as the message broker.

## Installation and Setup

Follow these steps to set up the project on your local machine.

### Prerequisites

Ensure you have the following installed:
- Python 3.x
- MySQL Database
- RabbitMQ (for Celery)
- Git
- Virtualenv (optional but recommended)

### Step 1: Clone the GitHub Repository

```bash
git clone https://github.com/your-username/alx_travel_app.git
cd alx_travel_app
```

### Step 2: Set Up a Virtual Environment

Create and activate a virtual environment (optional but recommended).

```bash
python3 -m venv venv
source venv/bin/activate
```

### Step 3: Install Dependencies

Install the required dependencies using `pip`.

```bash
pip install -r requirements.txt
```

The `requirements.txt` file contains the following key dependencies:
- `Django`
- `djangorestframework`
- `django-cors-headers`
- `celery`
- `rabbitmq`
- `drf-yasg`
- `django-environ` (for handling environment variables)

### Step 4: Configure Database Settings

Create a `.env` file in the project root directory to store sensitive information such as MySQL database credentials.

```ini
DATABASE_URL=mysql://username:password@localhost/dbname
```

Update your `settings.py` file to read from this `.env` file:

```python
import environ

# Initialize environment variables
env = environ.Env()
environ.Env.read_env()

# Database Configuration
DATABASES = {
    'default': env.db(),  # Automatically reads from DATABASE_URL in .env
}
```

### Step 5: Migrate Database

Run the following command to create the necessary database tables:

```bash
python manage.py migrate
```

### Step 6: Create a Superuser (Optional)

If you want to access the Django admin panel, you can create a superuser:

```bash
python manage.py createsuperuser
```

### Step 7: Run the Development Server

Start the Django development server:

```bash
python manage.py runserver
```

The API will be accessible at `http://localhost:8000/`. The Swagger API documentation will be available at `http://localhost:8000/swagger/`.

### Step 8: Set Up Celery with RabbitMQ

Make sure RabbitMQ is installed and running on your system. Then configure Celery to use RabbitMQ as the message broker.

In `settings.py`, configure Celery:

```python
CELERY_BROKER_URL = 'pyamqp://guest@localhost//'
CELERY_ACCEPT_CONTENT = ['json']
CELERY_TASK_SERIALIZER = 'json'
```

### Step 10: Verify Swagger Documentation

Visit `http://localhost:8000/swagger/` to view the automatically generated Swagger API documentation.

## Files Structure

Here’s an overview of the important files and directories in the project:

- **`alx_travel_app/`**: Root directory of the Django project.
  - **`requirements.txt`**: Contains the list of Python dependencies.
  - **`settings.py`**: Django project settings file.
  - **`urls.py`**: Main URL configuration file for the project.
  - **`listings/`**: The Django app for the project containing models, views, serializers, etc.

## Conclusion

This setup guide helps you configure the Django project with MySQL, integrate Swagger for API documentation, and set up Celery with RabbitMQ for asynchronous task management.


2. **Settings Grouped Logically**:
    - **App Configuration**: All apps (`INSTALLED_APPS`, `MIDDLEWARE`) are grouped together.
    - **Database & Passwords**: Database settings and password validation come together.
    - **Internationalization**: Language and timezone settings.
    - **Static & Media Files**: This section comes after internationalization settings.
    - **Celery & API**: Celery configurations and API settings such as `REST_FRAMEWORK` are placed last under the relevant sections.
3. **Secret Key & Debug**: These are now fetched from the environment as they should not be hardcoded in production.

This structure follows a conventional layout that helps with readability, organization, and maintenance. You can now proceed with further configuration as needed. Let me know if you'd like more help with this!
