# EX01 Developing a Simple Webserver

# Date:
# AIM:
To develop a simple webserver to serve html pages and display the configuration details of laptop.

# DESIGN STEPS:
## Step 1:
HTML content creation.

## Step 2:
Design of webserver workflow.

## Step 3:
Implementation using Python code.

## Step 4:
Serving the HTML pages.

## Step 5:
Testing the webserver.

# PROGRAM:

# views.py:

    from django.shortcuts import render
    import platform
    import psutil

    def laptop_config(request):
        config_details = {
            "System": platform.system(),
            "Node Name": platform.node(),
            "Release": platform.release(),
            "Version": platform.version(),
            "Machine": platform.machine(),
            "Processor": platform.processor(),
            "CPU Count": psutil.cpu_count(logical=True),
            "RAM": f"{round(psutil.virtual_memory().total / (1024 ** 3), 2)} GB",
        }
        return render(request, 'config/laptop_config.html', {'config': config_details})

# settings.py:

    from pathlib import Path


    BASE_DIR = Path(__file__).resolve().parent.parent


    SECRET_KEY = 'django-insecure--7-i(ecls_3beb$v(mi6m$9hc^q2_t6%v7!bup1eu0wwkhdnyc'

    DEBUG = True

    ALLOWED_HOSTS = []

    INSTALLED_APPS = [
        'django.contrib.admin',
        'django.contrib.auth',
        'django.contrib.contenttypes',
        'django.contrib.sessions',
        'django.contrib.messages',
        'django.contrib.staticfiles',
        'config',
    ]

    MIDDLEWARE = [
        'django.middleware.security.SecurityMiddleware',
        'django.contrib.sessions.middleware.SessionMiddleware',
        'django.middleware.common.CommonMiddleware',
        'django.middleware.csrf.CsrfViewMiddleware',
        'django.contrib.auth.middleware.AuthenticationMiddleware',
        'django.contrib.messages.middleware.MessageMiddleware',
        'django.middleware.clickjacking.XFrameOptionsMiddleware',
    ]

    ROOT_URLCONF = 'Lap_config.urls'

    TEMPLATES = [
        {
            'BACKEND': 'django.template.backends.django.DjangoTemplates',
            'DIRS': [],
            'APP_DIRS': True,
            'OPTIONS': {
                'context_processors': [
                    'django.template.context_processors.debug',
                    'django.template.context_processors.request',
                    'django.contrib.auth.context_processors.auth',
                    'django.contrib.messages.context_processors.messages',
                ],
            },
        },
    ]

    WSGI_APPLICATION = 'Lap_config.wsgi.application'


    DATABASES = {
        'default': {
            'ENGINE': 'django.db.backends.sqlite3',
            'NAME': BASE_DIR / 'db.sqlite3',
        }
    }

    AUTH_PASSWORD_VALIDATORS = [
        {
            'NAME': 'django.contrib.auth.password_validation.UserAttributeSimilarityValidator',
        },
        {
            'NAME': 'django.contrib.auth.password_validation.MinimumLengthValidator',
        },
        {
            'NAME': 'django.contrib.auth.password_validation.CommonPasswordValidator',
        },
        {
            'NAME': 'django.contrib.auth.password_validation.NumericPasswordValidator',
        },
    ]


    LANGUAGE_CODE = 'en-us'

    TIME_ZONE = 'UTC'

    USE_I18N = True

    USE_TZ = True

    STATIC_URL = 'static/'

    DEFAULT_AUTO_FIELD = 'django.db.models.BigAutoField'

# urls.py:

    from django.contrib import admin
    from django.urls import path, include

    urlpatterns = [
        path('admin/', admin.site.urls),
        path('', include('config.urls')),
    ]


# templates.html:

    <!DOCTYPE html>
    <html lang="en">
    <head>
        <meta charset="UTF-8">
        <meta name="viewport" content="width=device-width, initial-scale=1.0">
        <title>Laptop Configuration</title>
        <style>
        
            @import url('https://fonts.googleapis.com/css2?family=Roboto:wght@400;500;700&display=swap');

            
            body {
                font-family: 'Roboto', Arial, sans-serif;
                background: linear-gradient(135deg, #0f2027, #203a43, #2c5364); 
                background-size: 400% 400%;
                animation: gradientShift 15s ease infinite; 
                color: #e0e0e0;
                margin: 0;
                padding: 0;
                display: flex;
                justify-content: center;
                align-items: center;
                height: 100vh;
            }

        
            @keyframes gradientShift {
                0% { background-position: 0% 50%; }
                50% { background-position: 100% 50%; }
                100% { background-position: 0% 50%; }
            }

            
            .container {
                background: rgba(18, 18, 18, 0.9); 
                border-radius: 12px;
                box-shadow: 0 10px 30px rgba(0, 0, 0, 0.7); 
                padding: 40px 50px;
                max-width: 800px;
                width: 90%;
                position: relative;
                transition: transform 0.3s ease, box-shadow 0.3s ease;
            }
            .container:hover {
                transform: translateY(-5px);
                box-shadow: 0 15px 40px rgba(0, 0, 0, 0.9);
            }


            h1 {
                font-size: 28px;
                margin-bottom: 20px;
                text-align: center;
                color: #00bcd4; 
                border-bottom: 2px solid #00bcd4;
                display: inline-block;
                padding-bottom: 8px;
                text-transform: uppercase;
                letter-spacing: 1.2px;
            }

            
            table {
                width: 100%;
                border-collapse: collapse;
                margin-top: 20px;
            }
            th, td {
                text-align: left;
                padding: 15px 20px;
                border-bottom: 1px solid #444;
            }
            th {
                background-color: #1e272e; 
                color: #00bcd4; 
                font-weight: 600;
                text-transform: uppercase;
            }
            tr:nth-child(even) {
                background-color: #121212; 
            }
            tr:hover {
                background-color: #1e1e1e; 
            }
            td {
                font-size: 15px;
                color: #ddd; 
            }
            th:first-child, td:first-child {
                border-radius: 8px 0 0 8px;
            }
            th:last-child, td:last-child {
                border-radius: 0 8px 8px 0;
            }
            .footer {
                text-align: center;
                margin-top: 20px;
                font-size: 12px;
                color: #ec2323;
            }
        </style>
    </head>
    <body>
        <div class="container">

            <h1>Laptop Configuration Details</h1>    
            <table>
                <thead>
                    <tr>
                        <th>Property</th>
                        <th>Value</th>
                    </tr>
                </thead>
                <tbody>
                    {% for key, value in config.items %}
                    <tr>
                        <td>{{ key }}</td>
                        <td>{{ value }}</td>
                    </tr>
                    {% endfor %}
                </tbody>
            </table>
        </div>

        
        <div class="footer">
            © 2024 Laptop Configurations. Crafted for 6LI-1 Web Assingment.
        </div>
    </body>
    </html>


# OUTPUT:
![Result pic](output1.png)

# RESULT:
The program for implementing simple webserver is executed successfully.
