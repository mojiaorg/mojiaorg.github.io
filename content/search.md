---
title: "搜索"
layout: "search"
---

<script src="https://pagefind.com/pagefind/latest/pagefind-ui.js"></script>
<link rel="stylesheet" href="https://pagefind.com/pagefind/latest/pagefind-ui.css" />

<style>
  .search-container {
    max-width: 600px;
    margin: 2rem auto;
    padding: 0 1rem;
  }
  .search-container input {
    width: 100%;
    padding: 0.75rem 1rem;
    font-size: 1.1rem;
    border: 2px solid #ddd;
    border-radius: 8px;
    outline: none;
  }
  .search-container input:focus {
    border-color: #4a90d9;
  }
  .pagefind-ui__result {
    border-bottom: 1px solid #eee;
    padding: 1rem 0;
  }
  .pagefind-ui__result-title {
    font-size: 1.1rem;
    color: #333;
    text-decoration: none;
  }
  .pagefind-ui__result-excerpt {
    color: #666;
    margin-top: 0.5rem;
  }
</style>

<div class="search-container">
  <div id="search"></div>
</div>

<script>
  window.addEventListener('DOMContentLoaded', (event) => {
    new PagefindUI({ element: "#search", showSubResults: true });
  });
</script>
