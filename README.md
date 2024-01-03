# Laravel Envoy Deploy

This repository includes an Envoy.blade.php script that is designed to provide a basic "zero-downtime" deployment option using the open-source Laravel Envoy tool.

## Installation

`composer global require "laravel/envoy"`

## Usage

1. Copy the Envoy.blade.php file into the root of your Laravel project.

`wget https://raw.githubusercontent.com/papertank/envoy-deploy/master/Envoy.blade.php`

2. Setup .env, see .env.example for an example.

3. Run the INIT COMMAND to setup the server. (once only)

`envoy run init`

4. Run the DEPLOY COMMAND to deploy the latest version of your code.

`envoy run deploy`

5. See Envoy.blade.php for more commands.
