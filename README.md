# authentication-and-authorization

## System
1. Linux Ubuntu 20.04

## Installation

1. Clone repo to local

```
git clone https://github.com/aniket-k-kaushik/authentication-and-authorization.git
```

2. Install [rvm](https://rvm.io/) and
   [nvm](https://github.com/nvm-sh/nvm#installing-and-updating)

3. Install ruby 3.0.1

```
rvm install 3.0.1
```

4. Install Node 16.4.2

```
nvm install 16.4.2
```

5. Install Postgres

```
sudo apt install postgresql-12 libpq-dev
```

6. Create Username and password to access postgreSQL

```
sudo -u postgres createuser aniket -s   // In place of aniket you can give your name
```
```
sudo -u postgres psql
```
To set password for the new user we just created
```
postgres=# \password aniket   // aniket is the username 
```
Then Enter possword and re-enter it to confirm it.

7. Go to authentication-and-authorization/ds-assignment-backend

```
cd authentication-and-authorization/ds-assignment-backend
```

8. Install gem

```
bundle install
```

9. Install node packages

```
yarn install
```

10. Setup ENV's

Open .env

11. Update `DATABASE_URL` in `.env` as per local `psql` creds. For example, if
    the user is `aniket` and password is `aniket`, change the variable as
    `DATABASE_URL="postgres://aniket:aniket@localhost/ds-assignment-backend?encoding=utf8&pool=5&timeout=5000"`

12. Run `rake db:create` to create the database
```
rake db:create
```
14. Run `rake db:migrate` for migrations
```
rake db:migrate
```
16. Run `rake db:seed` for populating the database with initial data
```
rake db:seed
```

15. Run `rails s` to run rails server
```
rails s
```

16. Navigate to [http://127.0.0.1:3000/](http://127.0.0.1:3000/)

## Session based Authentication

17. It takes you to root page
    The `Sign In and Sign Up` are basic`devise` session based authentions.

The `{"name"=>"Web Client", "client_id"=>"NJkR6r9S5XlZyaqmWTwwWoZ4TM4j2dJssD5jkIZgIwY", "client_secret"=>"4hq0friqgrFaH0mxsY0szZHSbo2M-wLODIcGSxAXb7M"}`
is used in API `authentication` and `authorization`

![root_page](https://user-images.githubusercontent.com/94526737/171061682-ca757725-1335-4e97-bc88-f3178a125c9a.png)

18. SignUp link take us to the `Sign Up` page

![sign_up_devise](https://user-images.githubusercontent.com/94526737/171062095-65c9ac5e-8688-4d5f-84ca-4697971fea6d.png)

19. SignIn link takes us to the `Sign In` page

![sign_in_page](https://user-images.githubusercontent.com/94526737/171062177-2446c269-197e-4c6b-83a9-f5b0b8a506d2.png)

## API Based Authentication and Authorization

* For this we would need an Postman APP

### 20. To Register a User through API

* In postman app, copy and paste the URL and Request should be `POST`
* Go to `Header` Section of the postman app add `Content-Type` `application/json`
* Go to `Body` select `raw` and paste the below lines

````
{
   "email" : "aniket.kaushik@example.com",                            // email you would like to register
   "password" : "password",                                           // password you would like to regiter  
   "client_id" : "NJkR6r9S5XlZyaqmWTwwWoZ4TM4j2dJssD5jkIZgIwY"        // copy the client_id in the root page and replace it with the current string
}
````

* Copy the below link and page it in the postman `Enter Request URL` input box
```
http://127.0.0.1:3000/api/v1/users
```

* you can expect a similar kind of response
````
{
    "id": 3,
    "email": "aniket.test@example.com",
    "access_token": "-9dZnzOYHrn2o1FWgaqw6RjTu5YcAMniNAcg3wy-6YI",
    "token_type": "Bearer",
    "expires_in": 7200,
    "refresh_token": "496f3c806bfa1d2626cfddf8b67ab312e0a78b9b3ddaeecd70aa9e70d173d579",
    "created_at": 1653948033
}
````


![api_registration_user_request_response](https://user-images.githubusercontent.com/94526737/171063112-287479a2-a847-4f3d-a031-6ed567a15522.png)


### 21. To LogIn a User through API

* In postman app, copy and paste the URL and Request should be `POST`
* Go to `Header` Section of the postman app add `Content-Type` `application/json`
* Go to `Body` select `raw` and paste the below lines

````
{
   "grant_type" : "password",
   "email" : "aniket@example.com",
   "password" : "password",
   "client_id" : "NJkR6r9S5XlZyaqmWTwwWoZ4TM4j2dJssD5jkIZgIwY",
   "client_secret" : "4hq0friqgrFaH0mxsY0szZHSbo2M-wLODIcGSxAXb7M"
}

````

* Copy the below link and page it in the postman `Enter Request URL` input box
```
http://127.0.0.1:3000/api/v1/oauth/token
```

* you can expect a similar kind of response
````
{
    "access_token": "tR3CriKQhT24e5JQ05kSaJxF1jnl3aCW43bFGnR-JJQ",
    "token_type": "Bearer",
    "expires_in": 7200,
    "refresh_token": "t6FpPW-1Kw1p_kchsMwii1ruI_h6pHQI4x9MtJJYkaA",
    "created_at": 1653948364
}
````


![api_login_request_response](https://user-images.githubusercontent.com/94526737/171063522-ee853663-c1d0-460f-a4d3-64d91088060a.png)


### 21. To LogOut a User through API

* In postman app, copy and paste the URL and Request should be `POST`
* Go to `Header` Section of the postman app add `Content-Type` `application/json`
* Go to `Body` select `raw` and paste the below lines

````
{
   "token" : "UPML64iUotDeSjqLQBvTAuLB7DmVVla2TuGcg6Fb0Ek",
   "client_id" : "NJkR6r9S5XlZyaqmWTwwWoZ4TM4j2dJssD5jkIZgIwY",
   "client_secret" : "4hq0friqgrFaH0mxsY0szZHSbo2M-wLODIcGSxAXb7M"
}
````
* Copy the below link and page it in the postman `Enter Request URL` input box
```
http://127.0.0.1:3000/api/v1/oauth/revoke
```

* you can expect a similar kind of response

````
{}
````
