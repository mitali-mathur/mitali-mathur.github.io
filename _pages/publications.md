---
layout: page
permalink: /publications/
title: Research
description: My research interests lie at the intersection of migration, labor, and development economics. I am looking forward to pursuing these topics throughout my PhD. As of now, all of my prior research has been more policy-focused - I contributed to research projects in collaboration with organizations to support their work in generating evidence-based policy recommendations. Below is a sample of some of the projects I played a large role in.
nav: true
nav_order: 2
---
<!-- _pages/publications.md -->

<style>
  .research-tabs {
    display: flex;
    flex-wrap: wrap;
    gap: 0.5rem;
    margin-bottom: 2rem;
    border-bottom: 2px solid #dee2e6;
    padding-bottom: 0;
  }
  .research-tabs .tab-btn {
    background: none;
    border: none;
    border-bottom: 3px solid transparent;
    padding: 0.5rem 1rem;
    font-size: 0.95rem;
    font-weight: 500;
    color: #6c757d;
    cursor: pointer;
    transition: color 0.2s, border-color 0.2s;
    margin-bottom: -2px;
  }
  .research-tabs .tab-btn:hover {
    color: var(--global-theme-color, #2698BA);
  }
  .research-tabs .tab-btn.active {
    color: var(--global-theme-color, #2698BA);
    border-bottom-color: var(--global-theme-color, #2698BA);
  }
</style>

<div class="research-tabs">
  <button class="tab-btn active" data-filter="all">All</button>
  <button class="tab-btn" data-filter="Migration">Migration</button>
  <button class="tab-btn" data-filter="Data Quality & Methods">Data Quality & Methods</button>
  <button class="tab-btn" data-filter="Gender">Gender</button>
  <button class="tab-btn" data-filter="Behavioral Nudges">Behavioral Nudges</button>
</div>

<div class="publications">

{% bibliography -f papers %}

</div>

<script>
document.addEventListener("DOMContentLoaded", function () {
  var buttons = document.querySelectorAll(".research-tabs .tab-btn");
  var entries = document.querySelectorAll(".bib-entry");
  // Define the category order for the "All" tab
  var categoryOrder = ["Migration", "Data Quality & Methods", "Gender", "Behavioral Nudges"];

  buttons.forEach(function (btn) {
    btn.addEventListener("click", function () {
      // Update active button
      buttons.forEach(function (b) { b.classList.remove("active"); });
      btn.classList.add("active");

      var filter = btn.getAttribute("data-filter");

      if (filter === "all") {
        // Show all and reorder by category
        entries.forEach(function (entry) {
          entry.style.display = "";
          // Use category order as sort key
          var cat = entry.getAttribute("data-category") || "";
          var order = categoryOrder.indexOf(cat);
          entry.style.order = order >= 0 ? order : 999;
        });
      } else {
        entries.forEach(function (entry) {
          var cat = entry.getAttribute("data-category");
          if (cat === filter) {
            entry.style.display = "";
          } else {
            entry.style.display = "none";
          }
        });
      }

      // Hide/show the category group headers (h2.bibliography) and their lists
      document.querySelectorAll(".publications h2.bibliography").forEach(function (header) {
        var nextEl = header.nextElementSibling;
        while (nextEl && nextEl.tagName !== "H2" && !nextEl.matches("ol.bibliography")) {
          nextEl = nextEl.nextElementSibling;
        }
        if (nextEl && nextEl.matches("ol.bibliography")) {
          var visibleItems = nextEl.querySelectorAll(".bib-entry:not([style*='display: none'])");
          var show = visibleItems.length > 0;
          header.style.display = show ? "" : "none";
          nextEl.style.display = show ? "" : "none";
        }
      });
    });
  });
});
</script>