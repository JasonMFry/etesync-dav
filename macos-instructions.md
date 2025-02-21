## Configuration

* OSX
    * CalDAV: Works. Setup instructions:
      * Internet Accounts->Add Other Account->CalDAV account
      * Account Type: Advanced
      * Username: user@example.com
      * Password: generated etesync-dav password
      * Server Address: localhost
      * Server Path: /
      * Port: 37358
      * Check "Use SSL".
    * CardDAV: Works. Setup instructions:
      * Internet Accounts->Add Other Account->CardDAV account
      * Account Type: Manual
      * Username: user@example.com
      * Password: generated etesync-dav password
      * Server Address: `https://localhost:37358/` (please note it's https, not http!)

## macOS Mojave bugs

macOS Mojave suffers from a bug that enforces the use of SSL, *regardless* of whether you enable the checkbox for SSL or not. So to use EteSync, you have to enable SSL.

## Setup SSL

Instructions differ depending on how you run `etesync-dav`. Most people will just need the first.

### Webui

1. Login
2. Click on the "Setup SSL" button at the top and wait.
3. Enter your password once prompted by the system.
4. Restart `etesync-dav`

### Command line tool

1. Login
2. Run `etesync-dav certgen`
3. Enter your password once prompted by the system.
4. Restart `etesync-dav`

### Manual setup

Alternatively you can generate and configure a self-signed certificate manually with the following steps:

1. Generate a self-signed certificate (valid for 10 years)

````bash
cd ~/Library/Application\ Support/etesync-dav
openssl req -new -newkey rsa:4096 -days 3650 -nodes -x509 -subj "/CN=localhost" -keyout etesync.key -out etesync.crt
````

2. Using `open` command triggers macOS "add to keychain" dialog (equivelent of double-clicking that file in Finder):

````bash
open etesync.crt
````

3. In the dialog confirm adding to "login" keychain.
4. Open `Keychain Access` app, find and open `localhost` (under Keychains: login, Category: Certificates), expand "Trust" and pick "Always trust" for SSL.

5. Restart `etesync-dav`
