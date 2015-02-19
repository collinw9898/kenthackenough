# Kent Hack Enough
The world's best hackathon website.

## Installation
### Prerequisites
1. Install [MongoDB](http://docs.mongodb.org/manual/installation/)
1. Install [NodeJS](http://nodejs.org/)
1. `npm install -g npm`
1. `npm install -g n`
1. `n stable`

### Development
1. Clone this repository
1. `npm install`
1. `node app`

## Testing
1. `npm install -g mocha`
1. `npm test`

## API

### User
#### Register a new user
```javascript
POST /api/users/register
{
  email: String,
  password: String
}

RESPONSE:
{
  _id: String,
  email: String,
  password: String,
  role: String
}
```

#### Activate a user
**Note:** Currently deprecated (we're not requiring email verification)
```javascript
GET /api/users/activate/<user_id>

RESPONSE:
{}
```

#### Login a user (check their credentials)
```javascript
POST /api/users/login
{
  email: String,
  password: String
}

RESPONSE:
{
  email: String,
  password: String,
  role: String
}
```

#### Get a list of all users
```javascript
GET /api/users
HTTP Basic Auth (staff, admin)
```

#### Unsubscribe a user (remove them from mailing list)
```javascript
POST /api/users/unsubscribe
HTTP Basic Auth (staff, admin)
{
  userId: String
}
```

#### Completely delete a user (just in case!)
```javascript
POST /api/users/delete
HTTP Basic Auth (admin)
{
  userId: String
}
```

### Application

#### Submit an application
```javascript
POST /api/application/submit
HTTP Basic Auth (attendee, staff, admin)
{
  name: String,           // full name
  school: String,         // name of school
  phone: String,          // phone number
  shirt: String,          // t-shirt size
  demographic: Boolean,   // allowed to use demographic info?
  first: Boolean,         // is this your first hackathon?
  dietary: String,        // food restrictions seperated by |
  year: String,           // the year in school
  age: Number,            // person's age
  gender: String,         // gender
  major: String,          // degree
  conduct: Boolean,       // agree to MLH code of conduct?
  travel: Boolean,        // need travel reimbursement?
  waiver: Boolean         // agreed to waiver?
}

RESPONSE:
// the created application object
```

#### Update an application
```javascript
POST /api/application/update
HTTP Basic Auth (attendee, staff, admin)
{
  name: String,           // full name
  school: String,         // name of school
  phone: String,          // phone number
  shirt: String,          // t-shirt size
  demographic: Boolean,   // allowed to use demographic info?
  first: Boolean,         // is this your first hackathon?
  dietary: String,        // food restrictions seperated by |
  year: String,           // the year in school
  age: Number,            // person's age
  gender: String,         // gender
  major: String,          // degree
  conduct: Boolean,       // agree to MLH code of conduct?
  travel: Boolean,        // need travel reimbursement?
  waiver: Boolean         // agreed to waiver?
}

RESPONSE:
// the updated application object
```

#### RSVP to an application
```javascript
POST /api/application/rsvp
HTTP Basic Auth (attendee, staff, admin)
{
  going: Boolean
}

RESPONSE:
{}
```

#### Get an application
```javascript
GET /api/application
HTTP Basic Auth (attendee, staff, admin)

RESPONSE:
// the application object
```

#### Set an application status
```javascript
POST /api/application/status
HTTP Basic Auth (staff, admin)
{
  userId: String,
  status: 'approved'|'denied'|'waitlisted'|'pending'
}

RESPONSE:
// the updated application object
```

#### Softly remove a user's application
```javascript
POST /api/application/remove
HTTP Basic Auth (staff, admin)
{
  userId: String
}
```

#### Quickly register a user
```javascript
POST /api/application/quick
HTTP Basic Auth (staff, admin)
{
  name: String,
  email: String,
  phone: String
}
```