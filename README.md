# Password Generator

A secure and customizable password generator that allows users to create strong passwords based on their preferences. This application provides various options for generating passwords, ensuring both security and usability.

## Table of Contents

- [Features](#features)
- [Demo](#demo)
- [Installation](#installation)
- [Build](#build)
- [Configuration](#configuration)
- [Usage](#usage)

## Features

- **Customizable Password Length**: Choose the length of the generated password.
- **Character Options**: Select which types of characters to include:
  - Letters (Upper- and lowercase)
  - Numbers
  - Special characters
  - Option to avoid ambiguous characters (like 'l', '1', 'O', '0', etc.)
- **Regenerate Passwords**: Easily regenerate passwords with the click of a button.
- **User-Friendly Interface**: Simple and intuitive UI for easy interaction. Copy passwords directly to your clipboard.
- **Super Fast**: Generate as many passwords as you need, multiple at a time.

## Demo

You can try the latest version here: [pw.schosser.dev](https://pw.schosser.dev)

## Installation

Follow these steps to set up the project locally:

1. Clone the repository:
   ```bash
   git clone https://github.com:Dalabad/password-generator.git
   ```
2. Install all dependencies 
    ```bash
    npm install
    ```

## Build

The project is prepared to be run as a docker container. To build the container yourself run

```bash
docker build . -t password-generator
```

## Configuration

The following environment variables are used to configure the password generator's default settings:

| Name                              | Type    | Default Value              |
|-----------------------------------|---------|----------------------------|
| `VITE_PASSWORD_AMOUNT_DEFAULT`     | Number  | `1`                        |
| `VITE_PASSWORD_AMOUNT_OPTIONS`     | String  | `"1,5,10,20"`              |
| `VITE_PASSWORD_LENGTH_DEFAULT`     | Number  | `20`                       |
| `VITE_USE_LETTERS`                 | Boolean | `true`                     |
| `VITE_USE_NUMBERS`                 | Boolean | `true`                     |
| `VITE_USE_SPECIAL_CHARACTERS`      | Boolean | `true`                     |
| `VITE_AVOID_AMBIGUOUS_CHARACTERS`  | Boolean | `true`                     |

## Usage

Run the docker container in your prefered environment and access the hosted website.

```bash
docker run -d -P \
  -e VITE_PASSWORD_AMOUNT_DEFAULT=1 \
  -e VITE_PASSWORD_AMOUNT_OPTIONS="1,5,10,20" \
  -e VITE_PASSWORD_LENGTH_DEFAULT=20 \
  -e VITE_USE_LETTERS=true \
  -e VITE_USE_NUMBERS=true \
  -e VITE_USE_SPECIAL_CHARACTERS=true \
  -e VITE_AVOID_AMBIGUOUS_CHARACTERS=true \
  password-generator:latest
```