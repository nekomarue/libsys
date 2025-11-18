# Project Title: Library System

## Description / Overview

A web-based Library Management System built using Laravel for managing categories, authors, books, and book copies easily.

## Objectives

* To provide an organized system for managing library resources.
* To allow CRUD operations for categories, authors, books, and copies.
* To improve efficiency in tracking and organizing books.

## Features / Functionality

* Dashboard displaying total categories, authors, books, and copies
* Add, edit, delete, and view categories
* Add, edit, delete, and view authors
* Add, edit, delete, and view books with category and author assignment
* Manage book copies and availability status

## Installation Instructions

1. Clone the repository: `git clone <your-repo-url>`
2. Navigate to the project directory: `cd your-project-folder`
3. Install dependencies: `composer install`
4. Copy the example environment file: `cp .env.example .env`
5. Generate app key: `php artisan key:generate`
6. Configure database in `.env` file
7. Run database migrations: `php artisan migrate`
8. Serve the application: `php artisan serve`

## Usage

1. Open your terminal and run 'php artisan serve'.
3. Access the web app via 'http://127.0.0.1:8000'.
5. Navigate through dashboard to manage categories, authors, books, and book copies.

## Code Snippet
### Book Controller

    '''<?php

    namespace App\Http\Controllers;
    
    use Illuminate\Http\Request;
    use App\Models\Book;
    
    class BookController extends Controller
    {
        // Display all books
        public function index()
        {
            $books = Book::orderBy('id', 'desc')->paginate(10);
            return view('books.index', compact('books'));
        }

        public function create()
        {
            return view('books.create');
        }
    
        // Save a new book
        public function store(Request $request)
        {
            $request->validate([
                'title' => 'required|string|max:255',
                'author' => 'nullable|string|max:255',
                'isbn' => 'nullable|string|unique:books,isbn|max:20',
                'qty' => 'required|integer|min:1',
            ]);
    
            Book::create($request->only('title', 'author', 'isbn', 'qty'));
    
            return redirect()->route('books.index')->with('success', 'Book added successfully.');
        }
    
        public function show($id)
        {
            $book = Book::findOrFail($id);
            return view('books.show', compact('book'));
        }
    
        //Edit a book
        public function edit($id)
        {
            $book = Book::findOrFail($id);
            return view('books.edit', compact('book'));
        }
    
        // Update a book
        public function update(Request $request, $id)
        {
            $book = Book::findOrFail($id);
    
            $request->validate([
                'title' => 'required|string|max:255',
                'author' => 'nullable|string|max:255',
                'isbn' => 'nullable|string|unique:books,isbn,'.$book->id.'|max:20',
                'qty' => 'required|integer|min:1',
            ]);
    
            $book->update($request->only('title', 'author', 'isbn', 'qty'));
    
            return redirect()->route('books.index')->with('success', 'Book updated successfully.');
        }
    
        // Delete a book
        public function destroy($id)
        {
            $book = Book::findOrFail($id);
            $book->delete();
    
            return redirect()->route('books.index')->with('success', 'Book deleted successfully.');
        }
    }'''


### Book Model
    '''<?php

    namespace App\Models;

    use Illuminate\Database\Eloquent\Factories\HasFactory;
    use Illuminate\Database\Eloquent\Model;

    class Book extends Model
    {
        use HasFactory;

        protected $fillable = ['title', 'author', 'isbn', 'qty'];

        public function transactions()
        {
            return $this->hasMany(Transaction::class);
        }
    }'''
## Contributors

Baldoz, Kathlyn R.

## License

This project is licensed under the MIT License.
You are free to use, modify, and distribute this project for educational purposes.
