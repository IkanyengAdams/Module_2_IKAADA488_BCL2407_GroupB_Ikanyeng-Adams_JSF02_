# Svelte E-Commerce Application

This is a simple e-commerce application built with Svelte, utilizing the FakeStore API for product data. The application includes features like product listing, product search, category filtering, and sorting by price.

# Table of Contents
1.Features
2.Installation
3.Usage
4.Components
5.API

# Features
-Product Listing: Displays a list of products fetched from the FakeStore API.
-Product Details: View detailed information about a product.
-Search: Search for products by name.
-Category Filtering: Filter products by category.
-Sorting: Sort products by price (low to high or high to low).

# Installation
To run this project locally, follow these steps:

1. Clone the repository:
    git clone https://github.com/yourusername/svelte-ecommerce.git
    cd svelte-ecommerce
   
2. Install dependencies:
    npm install

3. Run the development server:
   npm run dev

# Usage

Components

# Product List Page
 -The home page displays a list of products. You can filter the products by category, search by product name, and sort by price.


# Product Details Page
 -Clicking on a product will take you to the product details page, which displays detailed information about the product.

 # App.svelte
  -This is the main component that sets up the routes for the application.

# Navbar.svelte
 -This component handles displaying the list of products, filtering, searching, and sorting.

# API
-This application uses the FakeStore API to fetch product data.
