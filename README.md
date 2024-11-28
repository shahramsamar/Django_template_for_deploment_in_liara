# Django Template for Deployment in Liara

This repository contains a Django project template that is optimized for deployment on [Liara](https://liara.ir). It provides a basic setup for a Django project that can easily be deployed to Liara's cloud infrastructure. The project includes integration with PostgreSQL, environment variable management, and support for static and media file handling.

## Features

- **Django Setup**: A basic Django project ready for production deployment.
- **PostgreSQL Integration**: PostgreSQL configuration for production database use.
- **Static and Media Files Handling**: Pre-configured static and media file management for production.
- **Environment Variables**: Use of `.env` file to securely manage configuration.
- **Deployment on Liara**: Optimized for deployment on [Liara](https://liara.ir) without Docker.

## Requirements

- **Python 3.8+**
- **Liara CLI**: [Install Liara CLI](https://docs.liara.ir/cli/installation)
- **PostgreSQL**: PostgreSQL for production database storage.

## Installation

1. **Clone the repository**:

    ```bash
    git clone https://github.com/shahramsamar/Django_template_for_deploment_in_liara.git
    cd Django_template_for_deploment_in_liara
    ```

2. **Set up your environment variables**:

    Create a `.env` file in the root directory with the following environment variables:

    ```bash
    SECRET_KEY=your-django-secret-key
    DEBUG=False
    ALLOWED_HOSTS=your-liara-domain.ir
    DATABASE_URL=postgres://username:password@host:port/database_name
    ```

    Replace the placeholder values with your actual configuration details.

3. **Install dependencies**:

    Create a virtual environment and install the required dependencies:

    ```bash
    python -m venv venv
    source venv/bin/activate  # On Windows, use `venv\Scripts\activate`
    pip install -r requirements.txt
    ```

4. **Run migrations**:

    Apply database migrations:

    ```bash
    python manage.py migrate
    ```

5. **Collect static files**:

    Prepare static files for production:

    ```bash
    python manage.py collectstatic
    ```

## Deployment Steps

1. **Install Liara CLI**

   If you haven’t already, install the Liara CLI tool following the [installation guide](https://docs.liara.ir/cli/installation).

2. **Log in to Liara**

   Log in to your Liara account using the following command:

    ```bash
    liara login
    ```

3. **Create a `liara.json` file**

    Create a `liara.json` file in the root directory with the following content:

    ```json
    {
      "type": "python",
      "name": "your-app-name"
    }
    ```

4. **Deploy the application**

    Deploy your Django app to Liara:

    ```bash
    liara deploy
    ```

    After deployment, your app will be live on your Liara domain.

## Additional Configuration

### PostgreSQL Setup on Liara

To use PostgreSQL, follow the steps in the [Liara PostgreSQL Guide](https://docs.liara.ir/postgresql/) to create a PostgreSQL database and update your `.env` file with the correct `DATABASE_URL` format.

### Static and Media Files

Ensure that your `settings.py` is correctly configured to handle static and media files for production:

```python
# settings.py

import os
from pathlib import Path

BASE_DIR = Path(__file__).resolve().parent.parent

STATIC_URL = '/static/'
STATIC_ROOT = BASE_DIR / 'staticfiles'

MEDIA_URL = '/media/'
MEDIA_ROOT = BASE_DIR / 'media'


