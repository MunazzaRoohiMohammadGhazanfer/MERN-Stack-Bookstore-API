# MERN-Stack-Bookstore-API 
```
// server.js
const express = require('express');
const app = express();
const mongoose = require('mongoose');

mongoose.connect('mongodb://localhost:27017/mydatabase', { useNewUrlParser: true, useUnifiedTopology: true });

const bookSchema = new mongoose.Schema({
  title: String,
  author: String
});

const Book = mongoose.model('Book', bookSchema);

app.get('/books', async (req, res) => {
  const books = await Book.find();
  res.json(books);
});

app.listen(3000, () => {
  console.log('Server started on port 3000');
});
```

```
jsx
// client.js
import React, { useState, useEffect } from 'react';
import axios from 'axios';

function App() {
  const [books, setBooks] = useState([]);

  useEffect(() => {
    axios.get('/books')
      .then(response => {
        setBooks(response.data);
      })
      .catch(error => {
        console.error(error);
      });
  }, []);

  return (
    <div>
      <h1>Books</h1>
      <ul>
        {books.map(book => (
          <li key={book._id}>{book.title} by {book.author}</li>
        ))}
      </ul>
    </div>
  );
}

export default App;
```
