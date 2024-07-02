# Project: Laravel Backend with Vue.js 3

[Check out the course at VueSchool.io](https://vueschool.io/courses/laravel-backends-for-vue-js-3).

## Tools

-   `scoop install main/docker`

    -   then, open a seperate PowerShell window as `administrator` and run:

        ```sh
        dockerd --register-service
        ```

-   `scoop install curl`
-   `scoop install openssl`
-   `scoop install extras/vcredist2022`
-   `scoop install php`
-   `scoop install main/composer`
-   `scoop install main/apache`
-   `scoop install extras/heidisql`

## Activate `openssl`

In your php installation dir,

-   rename `php.ini-development` to `php.ini`.
-   ucomment (e.g. remove the `;`) on the following lines:
    -   `extension=curl`
    -   `extension=fileinfo`
    -   `extension=openssl`
    -   and `extension_dir = "ext"`

## WSL On Windows

-   open a seperate PowerShell window as `administrator` and run: `Enable-WindowsOptionalFeature -Online -FeatureName Microsoft-Windows-Subsystem-Linux`
-   say `Y` to restart the computer
-   [download](https://learn.microsoft.com/en-us/windows/wsl/install-manual#step-4---download-the-linux-kernel-update-package) and install the `WSL2` package for Windows 11.
-   Enable the container feature, only if you have Windows Pro or Enterprise:
-   after the restart, run:

    ```sh
    wsl --install -d Ubuntu # Or any distribution you prefer
    ```

## Alternatively...

-   Get a server on Cloudways
-   Create a Laravel application
-   Under `Application Settings`, rename the app to `laravelcoursebackend`.
-   Once the app is created, under `Deployment via GIT`, create a SSH key.
-   Copy it
-   Over to GitHub, go `Settings` > `Deploy keys`.
-   Add a new deploy key
-   Go to the home page of the repo and copy the HTTPS clone URL: `https://github.com/JeremieLitzler/vueschool-course.git`
-   Back to the `Deployment via GIT` blade on Cloudways, paste the URL into `GIT Remote Address`
-   Click `Authenticate`
-   Select the branch and click `Deploy`

Note: every time the code changes, perform a pull in this blade and execute the database migration, if any.

### The first database migration

-   Connect through SSH to the server and browse to `laravelcoursebackend`:

    ```sh
    cd applications/laravelcoursebackend/public_html
    ```

-   Copy the `.env-example` to `.env`:

    ```sh
    cp .env.example .env
    ```

-   Edit the `.env` and replace the values of the following variables with the values found under the `Access Details` blade of the app:

    -   APP_URL: the url of the application
    -   DB_HOST: your server's IP address
    -   DB_DATABASE: the database name
    -   DB_USERNAME: the database username
    -   DB_PASSWORD: the database password

-   Save the file
-   Run the migration command:

    ```sh
    php artisan migrate
    ```

-   You should get:

    ```sh
    INFO  Preparing database.                                                                                                                                              Creating migration table ............................................. 34ms DONE                                                                                         INFO  Running migrations.                                                                                                                                              2014_10_12_000000_create_users_table ................................. 28ms DONE    2014_10_12_100000_create_password_reset_tokens_table ................. 27ms DONE    2014_10_12_100000_create_password_resets_table ...................... 105ms DONE    2014_10_12_200000_add_two_factor_columns_to_users_table .............. 59ms DONE    2019_08_19_000000_create_failed_jobs_table ........................... 18ms DONE    2019_12_14_000001_create_personal_access_tokens_table ................ 23ms DONE    2023_01_27_184241_create_links_table .................................. 7ms DONE
    ```

-   Under the `Access Details` blade of the app, click `Laucnh Database Manager` and check the tables are present!
