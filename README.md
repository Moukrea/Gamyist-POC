# Gamyist-POC

Angular/Symfony bootcamp final project

Manage your video game collection with full informations about your games, create wishlists and follow your gamelog. This also can be used as a video game database.

The app connects to an external API in order to fetch informations about the requested game. If found, it adds it to the internal database, otherwise, the user can create its own entry.

It has been made within 10 days of lessons, and some free time.

This is actually a POC of a much larger scale project, with much more data and functionnalities. In this current state, the app is not advised to be used as if it was fully functionnal... Though on the user side, it just works, there are some security concerns about user shares (privacy) and some quirks are still going on (just like on admin side).



## What you need

Composer, Node.js,  Angular CLI, OpenSSL
Also, to be able to use it, your SQL server must be running.



## How to install?

Simple clone this repository wherever you want `git clone --recurse-submodules https://github.com/Moukrea/Gamyist-POC.git` 

With a terminal in the `symfony` subfolder run the following:  
`composer install`  

Then we will set the keys for JWT and setup the database. Open the `.env` file (into the `symfony` subfolder) and in your terminal run:  
`mkdir -p config/jwt`  
`openssl genpkey -out config/jwt/private.pem -aes256 -algorithm rsa -pkeyopt rsa_keygen_bits:4096` (when asked, copy and paste the JWT_PASSPHRASE from the `.env` file, line 42)  
`openssl pkey -in config/jwt/private.pem -out config/jwt/public.pem -pubout` (when asked, copy and paste the JWT_PASSPHRASE from the `.env` file, line 42)  

Then in your `.env` file, adjust your database (line 32) settings according to your own :  
`DATABASE_URL=mysql://YourUsername:YourPassword@127.0.0.1:3306/gamyist?serverVersion=5.7`


To finish the Symfony side setup, run the following:  

`php bin/console doctrine:database:create`  
`php bin/console make:migration`  
`php bin/console doctrine:migrations:migrate`  
`php bin/console doctrine:fixtures:load`   
`php -S localhost:3000 -t public`  

For Angular, it's way shorter, just run the following commands:  
`npm install`  
`ng serve`  

You're all set!

## How to use?

To visit the Symfony backend, just go to localhost:3000  
For Angular, go to localhost:4200

You can use the admin as a sample account on both sides (Nickname: admin, Password: password)

The game library is just fixtures, why not try to fill it up with real data? Go to the game section on the Angular side and search for a popular retro game, you'll see... adding games to the library is a breathe!

All fake users share the same password (password), but their names are generated randomly (except admin)

Once loged (on Angular) you can add games to the library, edit the ones you added yourself (if you're admin, you can edit them all)... add games to you collection (as original, dematerialized, ROM), to your wishlist or gamelog on the fly (in each game details). If you're browsing you own collection, you'll also have quick menus to manage your collection directly from the list.

On the back-office, just a quick view of last additions, management of each CRUD (platforms, games, genres, users) and that's pretty much it.

From now on, to use it, just start a PHP server from the `symfony` folder using `php -S localhost:3000 -t public` and from the `angular` folder, run `ng serve`.