---
title: 'Home'
draft: false
---

# test 

<div class="container" id="recipe-container">
    <!-- Barre de recherche -->
    <div id="search-container" style="margin: 20px 0;">
        <input type="text" id="searchInput" placeholder="Rechercher une recette..." style="width: 100%; padding: 10px; font-size: 16px; border-radius: 5px; border: 1px solid #ccc;">
        <ul id="searchResults" style="list-style: none; padding: 0; margin-top: 10px;"></ul>
    </div>
</div>

<script>
    document.getElementById('searchInput').addEventListener('keyup', function() {
        var query = this.value.toLowerCase();
        fetch('/search.json')
            .then(response => response.json())
            .then(pages => {
                var results = pages.filter(page => page.title.toLowerCase().includes(query) || page.content.toLowerCase().includes(query));
                var resultsList = document.getElementById('searchResults');
                resultsList.innerHTML = '';
                results.forEach(result => {
                    var li = document.createElement('li');
                    var link = document.createElement('a');
                    link.href = result.link;
                    link.textContent = result.title;
                    li.appendChild(link);
                    resultsList.appendChild(li);
                });
            });
    });
</script>
