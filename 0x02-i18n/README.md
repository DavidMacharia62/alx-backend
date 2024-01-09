# Flask Localization and Internationalization

## Introduction

This repository provides a comprehensive guide on how to parametrize Flask templates for displaying content in different languages. Additionally, it covers techniques for inferring the correct locale based on various factors such as URL parameters, user settings, or request headers. Furthermore, the guide includes instructions on how to localize timestamps in your Flask application.

## Table of Contents

1. [Getting Started](#getting-started)
    1. [Prerequisites](#prerequisites)
    2. [Installation](#installation)

2. [Flask Template Parametrization](#flask-template-parametrization)
    1. [Template Setup](#template-setup)
    2. [Parametrizing Templates](#parametrizing-templates)

3. [Locale Inference](#locale-inference)
    1. [URL Parameters](#url-parameters)
    2. [User Settings](#user-settings)
    3. [Request Headers](#request-headers)

4. [Timestamp Localization](#timestamp-localization)
    1. [Date Formatting](#date-formatting)
    2. [Timezone Considerations](#timezone-considerations)

## 1. Getting Started

### 1.1 Prerequisites

Before you begin, ensure you have the following installed:

- Python (>=3.6)
- Flask

### 1.2 Installation

1. Clone this repository:

    ```bash
    git clone https://github.com/your-username/flask-localization.git
    ```

2. Navigate to the project directory:

    ```bash
    cd flask-localization
    ```

3. Install dependencies:

    ```bash
    pip install -r requirements.txt
    ```

## 2. Flask Template Parametrization

### 2.1 Template Setup

Ensure your Flask application is configured to use templates. Create a `templates` directory in your project and place your HTML templates inside it.

### 2.2 Parametrizing Templates

In your templates, use Flask's template syntax to parametrize content. For example:

```html
<!DOCTYPE html>
<html lang="{{ current_locale }}">
<head>
    <meta charset="UTF-8">
    <title>{{ get_text('page_title') }}</title>
</head>
<body>
    <h1>{{ get_text('welcome_message') }}</h1>
    <!-- Other content goes here -->
</body>
</html>
```

## 3. Locale Inference

### 3.1 URL Parameters

Extract the language from the URL and set the locale accordingly. Update your Flask routes to include the language parameter:

```python
@app.route('/<lang_code>/home')
def home(lang_code):
    set_locale(lang_code)
    # Rest of the route logic
```

### 3.2 User Settings

Implement user-specific settings for language preference. Store user preferences in a database and retrieve them during user authentication.

### 3.3 Request Headers

Inspect the `Accept-Language` header in incoming requests to determine the preferred language:

```python
def get_user_locale():
    user_languages = request.accept_languages
    # Logic to choose the appropriate language
    return chosen_locale
```

## 4. Timestamp Localization

### 4.1 Date Formatting

Use Flask-Babel for date formatting. Install it by adding the following to your `requirements.txt`:

```plaintext
Flask-Babel==2.0.0
```

In your application, initialize Babel and use it for date formatting:

```python
from flask_babel import Babel

babel = Babel(app)

@babel.localeselector
def get_locale():
    # Your locale selection logic here
    return chosen_locale
```

### 4.2 Timezone Considerations

When working with timestamps, ensure proper timezone handling. Use libraries like `pytz` to manage timezones consistently across your application.

```python
import pytz
from datetime import datetime

def localize_timestamp(timestamp, user_timezone):
    # Convert timestamp to user's timezone
    localized_time = timestamp.astimezone(pytz.timezone(user_timezone))
    return localized_time
```

## Conclusion

By following this guide, you will be equipped with the knowledge and tools to effectively parametrize Flask templates, infer the correct locale, and localize timestamps in your Flask application. Feel free to explore additional Flask extensions and libraries to enhance and customize your localization and internationalization features.
