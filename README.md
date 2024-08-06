# Django Two-Step Verification

## Overview

`django-two-step-verification` is a Django package that provides two-step verification (also known as two-factor authentication) for your Django applications. This package enhances the security of user authentication by requiring an additional verification step, ensuring that only authorized users can access your application.

## Features

- Easy integration with existing Django projects
- Supports multiple verification methods (e.g., email, SMS, authenticator apps)
- Configurable verification workflows
- Secure and reliable verification code generation and validation
- User-friendly interfaces for entering and managing verification codes
- Customizable templates and messages

## Installation

To install `django-two-step-verification`, simply run:

```sh
pip install django-two-step-verification
```

## Configuration

1. Add `two_step_verification` to your `INSTALLED_APPS` in the Django settings file:

```python
INSTALLED_APPS = [
    ...
    'two_step_verification',
]
```

2. Run the migrations to create the necessary database tables:

```sh
python manage.py migrate
```

3. Configure the verification methods and other settings in your Django settings file:

```python
TWO_STEP_VERIFICATION_METHODS = [
    'email',
    'sms',
    'authenticator_app',
]

TWO_STEP_VERIFICATION_SETTINGS = {
    'EMAIL_BACKEND': 'django.core.mail.backends.smtp.EmailBackend',
    'SMS_BACKEND': 'your.sms.backend',
    'AUTHENTICATOR_APP_ISSUER': 'YourAppName',
}
```

## Usage

### Enabling Two-Step Verification

To enable two-step verification for a user, call the `enable_two_step_verification` method:

```python
from two_step_verification.utils import enable_two_step_verification

user = User.objects.get(username='example')
enable_two_step_verification(user)
```

### Verifying Codes

During the login process, after verifying the username and password, prompt the user to enter the verification code:

```python
from two_step_verification.utils import verify_code

if verify_code(user, code):
    # Code is valid, proceed with login
    login(request, user)
else:
    # Code is invalid, prompt user to try again
```

### Customizing Templates

You can customize the templates for the verification process by overriding the default templates in your Django project. The default templates are located in the `two_step_verification/templates/two_step_verification/` directory.

## Contributing

Contributions are welcome! Please fork the repository and submit a pull request with your changes. For major changes, please open an issue first to discuss what you would like to change.

## License

This project is licensed under the MIT License - see the [LICENSE](LICENSE) file for details.
