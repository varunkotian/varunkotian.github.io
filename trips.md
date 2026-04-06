---
layout: page
title: Trips
permalink: /trips/
---

<style>
  /* Match the dark, high-contrast trip reading theme */
  body, .page-content, .wrapper {
    background-color: #1e1e1e !important;
    color: #e0e0e0 !important;
    font-family: -apple-system, BlinkMacSystemFont, "Segoe UI", Roboto, Helvetica, Arial, sans-serif !important;
    font-size: 18px !important;
    line-height: 1.6 !important;
  }

  h1, h2, h3, h4, h5, h6 {
    color: #ffffff !important;
    font-weight: bold !important;
    margin-top: 1.2em !important;
  }

  a {
    color: #4da6ff !important;
    text-decoration: underline !important;
  }

  li {
    margin-bottom: 0.6em !important;
  }

  .trip-search {
    margin: 1.2rem 0 0.8rem 0;
  }

  .trip-search label {
    display: block;
    color: #ffffff !important;
    font-weight: 600;
    margin-bottom: 0.4rem;
  }

  .trip-search input {
    width: 100%;
    max-width: 520px;
    background-color: #2d2d2d;
    color: #e0e0e0;
    border: 1px solid #4b4b4b;
    border-radius: 8px;
    padding: 0.65rem 0.8rem;
    font-size: 1rem;
    outline: none;
  }

  .trip-search input:focus {
    border-color: #4da6ff;
    box-shadow: 0 0 0 2px rgba(77, 166, 255, 0.25);
  }

  .trip-search-count {
    margin-top: 0.45rem;
    color: #c8c8c8;
    font-size: 0.95rem;
  }

  .trip-empty {
    display: none;
    margin-top: 0.7rem;
    color: #ffb3b3;
  }
</style>

Welcome to the trip directory. Use the links below to open each itinerary.

## Trip List

<div class="trip-search">
  <label for="tripSearch">Search trips</label>
  <input id="tripSearch" type="search" placeholder="Type a title, city, or keyword..." aria-label="Search trips">
  <p id="tripSearchCount" class="trip-search-count"></p>
</div>

- [Germany Road Trip Itinerary - Black Forest](/trip-blackforest/)  
  A 7-day road trip from Delft through Koblenz, Baden-Baden, Freiburg, Titisee, and Heidelberg.



<p id="tripEmpty" class="trip-empty">No trips matched your search.</p>

<script>
  (function () {
    var input = document.getElementById("tripSearch");
    var list = null;
    var count = document.getElementById("tripSearchCount");
    var empty = document.getElementById("tripEmpty");
    var searchBox = document.querySelector(".trip-search");

    if (searchBox) {
      var candidate = searchBox.nextElementSibling;
      while (candidate && candidate.tagName !== "UL") {
        candidate = candidate.nextElementSibling;
      }
      list = candidate;
    }

    if (!input || !list) {
      return;
    }

    var items = Array.prototype.slice.call(list.querySelectorAll("li"));

    function updateFilter() {
      var query = input.value.toLowerCase().trim();
      var visible = 0;

      items.forEach(function (item) {
        var text = item.textContent.toLowerCase();
        var show = query === "" || text.indexOf(query) !== -1;
        item.style.display = show ? "" : "none";

        if (show) {
          visible += 1;
        }
      });

      if (count) {
        count.textContent = String(visible) + (visible === 1 ? " trip shown" : " trips shown");
      }

      if (empty) {
        empty.style.display = visible === 0 ? "block" : "none";
      }
    }

    input.addEventListener("input", updateFilter);
    updateFilter();
  })();
</script>
