# # Chimoney Laravel SDK Documentation

Welcome to the Chimoney Laravel SDK! This guide will help you install, set up, and use the SDK effectively to integrate Chimoney API functionality into your Laravel application.

---

## Installation Instructions

### Prerequisites
Before installing the Chimoney Laravel SDK, ensure the following:

- Laravel version 8.x or higher is installed.
- PHP 7.4 or higher is installed.
- Composer is installed for managing dependencies.

### Install the Package

To install the Chimoney Laravel SDK, run the following command using Composer:

```bash
composer require chimoney/laravel-sdk
```

### Publish Configuration File

After installing the package, publish the configuration file using the Artisan command:

```bash
php artisan vendor:publish --tag=chimoney-config
```

This will create a configuration file at `config/chimoney.php`.

---

## Configuration Details

### Set Environment Variables

Add the following entries to your `.env` file:

```env
CHIMONEY_API_KEY=your_api_key_here
CHIMONEY_BASE_URL=https://api.chimoney.io
```

- Replace `your_api_key_here` with your Chimoney API key.
- `CHIMONEY_BASE_URL` should point to the Chimoney API endpoint (default: `https://api.chimoney.io`).

### Configure the Package

The configuration file at `config/chimoney.php` should automatically use the `.env` variables. If you need to customize settings, modify the file as needed:

```php
return [
    'api_key' => env('CHIMONEY_API_KEY'),
    'base_url' => env('CHIMONEY_BASE_URL', 'https://api.chimoney.io'),
];
```

---

## Usage Guide

### Authentication

The SDK automatically handles authentication using the API key provided in your `.env` file.

### Basic Example: Fetching Account Balance

Here’s a simple example to fetch your Chimoney account balance:

```php
use Chimoney\LaravelSDK\Chimoney;

$chimoney = new Chimoney();
$response = $chimoney->getAccountBalance();

if ($response->success) {
    echo 'Account Balance: ' . $response->data->balance;
} else {
    echo 'Error: ' . $response->message;
}
```

### Sending a Payout Request

To send a payout, use the `sendPayout` method:

```php
$payoutDetails = [
    'recipient_email' => 'recipient@example.com',
    'amount' => 100.00,
    'currency' => 'USD',
];

$response = $chimoney->sendPayout($payoutDetails);

if ($response->success) {
    echo 'Payout successful! Transaction ID: ' . $response->data->transaction_id;
} else {
    echo 'Error: ' . $response->message;
}
```

---

## Testing Instructions

### Verifying Installation

1. Ensure the package is installed correctly by running:
   
   ```bash
   composer show chimoney/laravel-sdk
   ```

2. Check that the configuration file exists in `config/chimoney.php`.

### Running a Test Request

Use the following code snippet to verify that the SDK is functioning:

```php
use Chimoney\LaravelSDK\Chimoney;

$chimoney = new Chimoney();
$response = $chimoney->ping();

if ($response->success) {
    echo 'Chimoney SDK is working correctly!';
} else {
    echo 'Error: ' . $response->message;
}
```

### Troubleshooting

- **Missing API Key**: Ensure `CHIMONEY_API_KEY` is set in the `.env` file.
- **Connection Errors**: Verify that `CHIMONEY_BASE_URL` is correct and that your application can connect to the Chimoney API.
- **Debugging Requests**: Enable Laravel debug mode in `.env` to view detailed logs:

  ```env
  APP_DEBUG=true
  ```

For further assistance, contact Chimoney support or refer to the [official documentation](https://chimoney.io/docs).

---

With this guide, you should be able to seamlessly integrate Chimoney's SDK into your Laravel application. Happy coding!
