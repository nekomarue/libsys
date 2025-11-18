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

1. Open your terminal and run `php artisan serve`.
2. Access the web app via `http://127.0.0.1:8000`.
3. Navigate through dashboard to manage categories, authors, books, and book copies.

## Example (Book Controller Code)

    '''public function index()
    {
        $books = Book::orderBy('id', 'desc')->paginate(10);
        return view('books.index', compact('books'));
    }'''
    
## Contributors

Baldoz, Kathlyn R.

## License

This project is licensed under the MIT License.
You are free to use, modify, and distribute this project for educational purposes.
