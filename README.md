# Dataset Pagination Guide

## Introduction

This README file provides a detailed guide on paginating a dataset using simple page and page_size parameters, incorporating hypermedia metadata for enhanced navigation, and ensuring deletion-resilient pagination.

### Table of Contents

1. [Simple Pagination](#simple-pagination)
2. [Hypermedia Metadata](#hypermedia-metadata)
3. [Deletion-Resilient Pagination](#deletion-resilient-pagination)

## 1. Simple Pagination

### 1.1 Overview

Simple pagination involves breaking down a large dataset into smaller, manageable chunks using two main parameters: `page` and `page_size`.

### 1.2 Implementation

#### 1.2.1 Request Format

To request a specific page with a specified page size, make a GET request to your API endpoint with the following parameters:

- `page`: The page number (1-based index).
- `page_size`: The number of items per page.

Example:
```bash
GET /api/data?page=2&page_size=10
```

#### 1.2.2 Response Format

The API response will contain the paginated dataset along with metadata indicating the current page, total pages, total items, and links to navigate to other pages.

Example Response:
```json
{
  "data": [...],  // Paginated dataset
  "meta": {
    "page": 2,
    "total_pages": 5,
    "total_items": 50,
    "links": {
      "first": "/api/data?page=1&page_size=10",
      "prev": "/api/data?page=1&page_size=10",
      "next": "/api/data?page=3&page_size=10",
      "last": "/api/data?page=5&page_size=10"
    }
  }
}
```

## 2. Hypermedia Metadata

### 2.1 Overview

Hypermedia metadata enhances pagination by including links in the API response, allowing clients to navigate through pages seamlessly.

### 2.2 Implementation

#### 2.2.1 HATEOAS Links

- `first`: Link to the first page.
- `prev`: Link to the previous page.
- `next`: Link to the next page.
- `last`: Link to the last page.

#### 2.2.2 Example

```json
{
  "data": [...],
  "meta": {
    "page": 2,
    "total_pages": 5,
    "total_items": 50,
    "links": {
      "first": "/api/data?page=1&page_size=10",
      "prev": "/api/data?page=1&page_size=10",
      "next": "/api/data?page=3&page_size=10",
      "last": "/api/data?page=5&page_size=10"
    }
  }
}
```

## 3. Deletion-Resilient Pagination

### 3.1 Overview

Deletion-resilient pagination ensures stable navigation even when items are deleted from the dataset.

### 3.2 Implementation

#### 3.2.1 Unique Identifiers

Use unique identifiers for each item in the dataset. When an item is deleted, the identifier ensures consistency in pagination.

#### 3.2.2 Example

```json
{
  "data": [...],
  "meta": {
    "page": 2,
    "total_pages": 5,
    "total_items": 50,
    "links": {
      "first": "/api/data?page=1&page_size=10",
      "prev": "/api/data?page=1&page_size=10",
      "next": "/api/data?page=3&page_size=10",
      "last": "/api/data?page=5&page_size=10"
    }
  }
}
```

## Conclusion

This README provides a comprehensive guide on implementing simple pagination, enhancing it with hypermedia metadata, and ensuring deletion-resilient pagination. Feel free to adapt the examples to your specific API and dataset.
