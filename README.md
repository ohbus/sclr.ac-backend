# sclr.ac-backend
Backend for sclr.ac URL shortner 

[![Node.JS CI Status](https://github.com/scaleracademy/sclr.ac-backend/actions/workflows/node.js.yml/badge.svg)](https://github.com/scaleracademy/sclr.ac-backend/actions/workflows/node.js.yml)
[![Maintainability Rating](https://sonarcloud.io/api/project_badges/measure?project=scaleracademy_sclr.ac-backend&metric=sqale_rating)](https://sonarcloud.io/dashboard?id=scaleracademy_sclr.ac-backend)
[![Code Smells](https://sonarcloud.io/api/project_badges/measure?project=scaleracademy_sclr.ac-backend&metric=code_smells)](https://sonarcloud.io/dashboard?id=scaleracademy_sclr.ac-backend)
[![Maintainability](https://api.codeclimate.com/v1/badges/0a5878b3269471925751/maintainability)](https://codeclimate.com/github/scaleracademy/sclr.ac-backend/maintainability)
[![Codacy Badge](https://app.codacy.com/project/badge/Grade/3273a2cb0cd64893bf40886460fc0fa9)](https://www.codacy.com/gh/scaleracademy/sclr.ac-backend/dashboard?utm_source=github.com&amp;utm_medium=referral&amp;utm_content=scaleracademy/sclr.ac-backend&amp;utm_campaign=Badge_Grade)

## Development 

### API Endpoints 

#### `GET /{shortcode}`

Generate 302 redirect to longURL of that shortcode  

#### `POST /api/urls` 
Request 
```json
{
    "url": "https://some.long.url/of/long/length"
}
```

Success Response (status: `201`)
```json 
{
    "status": "success", 
    "data": {
        "shortCode": "kb24JO7",
        "shortLink": "https://sclr.ac/kb24JO7"
    }
}
```

Create new short code url (this will assign a random short code)

#### `PUT /api/urls/{shortcode}`
Create a new shortcode with the given one 
Request 
```json
{
    "url": "https://some.long.url/of/long/length"
}
```

Success Response (status: `201`)
```json 
{
    "status": "success", 
    "data": {
        "shortCode": "{shortcode}",
        "shortLink": "https://sclr.ac/{shortcode}"
    }
}
```


#### `GET /api/urls/{shortcode}`
Get details about a short code 

Error Response (status: `400` ) 
```json
{
    "status": "error",
    "message": "Invalid short Code, too long!"
}
```

Error Response (status: `404`) 
```json
{
    "status": "error",
    "message": "Invalid short code. Not found in DB"
}
```

Success Response (status: `200`)
```json 
{
    "status": "success", 
    "data": {
        "shortCode": "{shortcode}",
        "shortLink": "https://sclr.ac/{shortcode}"
    }
}
```

### Database 

#### Setup 

Setup database, user for this project

```postgres
create database sclrac; 
create user sclrac with encrypted password 'sclrac';
grant all privileges on database sclrac to sclrac;
```

#### Schema 

##### ShortCodes 

1. id 
2. shortcode
3. longUrl 
