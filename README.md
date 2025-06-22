# Library Management System

A RESTful API for managing books and borrowing operations built with Node.js, Express, TypeScript, and MongoDB.

## Features

- **Book Management**: Create, read, update, and delete books
- **Borrowing System**: Borrow books with automatic copy management
- **Automatic Status Updates**: Books automatically become unavailable when all copies are borrowed
- **Data Validation**: Input validation using Zod schemas
- **TypeScript**: Full type safety throughout the application
- **MongoDB**: Persistent data storage with Mongoose ODM

## Tech Stack

- **Runtime**: Node.js
- **Framework**: Express.js 5.x
- **Language**: TypeScript
- **Database**: MongoDB with Mongoose
- **Validation**: Zod
- **Development**: ts-node-dev for hot reloading

## Project Structure

```
src/
├── app/
│   ├── controllers/
│   │   ├── book.controller.ts      # Book CRUD operations
│   │   └── borrow.controller.ts    # Borrowing operations
│   ├── interface/
│   │   ├── book.interface.ts       # Book TypeScript interfaces
│   │   └── borrow.controllers.ts   # Borrow TypeScript interfaces
│   └── models/
│       ├── book.model.ts           # Book Mongoose model
│       └── borrow.model.ts         # Borrow Mongoose model
├── app.ts                          # Express app configuration
└── server.ts                       # Server entry point
```

## Installation

1. Clone the repository:
```bash
git clone <repository-url>
cd B5A3
```

2. Install dependencies:
```bash
npm install
```

3. Set up MongoDB:
   - Ensure MongoDB is running locally or update the connection string in your environment

4. Start the development server:
```bash
npm run dev
```

The server will start on `http://localhost:3000` (or the port specified in your environment).

## API Endpoints

### Books

#### Create a Book
```http
POST /api/books
Content-Type: application/json

{
  "title": "The Great Gatsby",
  "author": "F. Scott Fitzgerald",
  "genre": "FICTION",
  "isbn": "978-0743273565",
  "description": "A story of the fabulously wealthy Jay Gatsby",
  "copies": 5,
  "available": true
}
```

#### Get All Books
```http
GET /api/books?filter=FICTION&sortBy=title&sort=asc&limit=10
```

#### Get Book by ID
```http
GET /api/books/:bookId
```

#### Update Book
```http
PATCH /api/books/:bookId
Content-Type: application/json

{
  "copies": 3,
  "description": "Updated description"
}
```

#### Delete Book
```http
DELETE /api/books/:bookId
```

### Borrowing

#### Borrow a Book
```http
POST /api/borrow
Content-Type: application/json

{
  "book": "64f1a2b3c4d5e6f7g8h9i0j1",
  "quantity": 2,
  "dueDate": "2024-01-15"
}
```

#### Get Borrowing Summary
```http
GET /api/borrow
```

## Book Genres

Supported book genres:
- `FICTION`
- `NON_FICTION`
- `SCIENCE`
- `HISTORY`
- `BIOGRAPHY`
- `FANTASY`

## Key Features

### Automatic Copy Management
When books are borrowed, the system automatically:
- Reduces the available copies
- Updates the book's availability status to `false` when copies reach 0
- Uses both static and instance methods for flexible status updates

### Data Validation
All API endpoints use Zod schemas for input validation:
- Required fields validation
- Data type checking
- Enum validation for genres
- Date format validation for due dates

### Error Handling
Comprehensive error handling with:
- HTTP status codes
- Descriptive error messages
- Validation error details

## Development

### Scripts

- `npm run dev`: Start development server with hot reloading
- `npm test`: Run tests (to be implemented)

### TypeScript Configuration
The project uses strict TypeScript configuration with:
- ES2016 target
- CommonJS modules
- Strict type checking enabled

## Database Models

### Book Model
```typescript
{
  title: string;
  author: string;
  genre: "FICTION" | "NON_FICTION" | "SCIENCE" | "HISTORY" | "BIOGRAPHY" | "FANTASY";
  isbn: string;
  description?: string;
  copies: number;
  available: boolean;
}
```

### Borrow Model
```typescript
{
  book: ObjectId;
  quantity: number;
  dueDate: Date;
}
```

## Contributing

1. Fork the repository
2. Create a feature branch
3. Make your changes
4. Add tests if applicable
5. Submit a pull request

## License

ISC License

## Author

[Your Name]

---

For questions or support, please open an issue in the repository. 