---
title: "Bingo!"
weight: 5
---

# Bingo!

Print this out and see if you can get bingo within the week. Refresh to generate a new card. There are currently **{numsquares}** possible squares.

The list of possible squares lives in [this Google Sheet](https://docs.google.com/spreadsheets/d/1XXE3Mn8EK_SGeF77HlJAzNM6_V4cv6-COHoOJh62WsQ/edit?usp=sharing). Certain officers can modify this list. To suggest new content (or to object to existing content), contact one of them.

<div id="card">
</div>

<script src="https://cdn.jsdelivr.net/npm/papaparse@5.3.0/papaparse.min.js"></script>

<script>
    const shuffle = function(array) {
        for(let i = array.length - 1; i > 0; i--){
            const j = Math.floor(Math.random() * i)
            const temp = array[i]
            array[i] = array[j]
            array[j] = temp
        }
        return array;
    }

    const replaceText = function(oldtxt, newtxt) {
        var html = document.querySelector('html');
        var walker = document.createTreeWalker(html, NodeFilter.SHOW_TEXT);
        var node;
        while (node = walker.nextNode()) {
            node.nodeValue = node.nodeValue.replace(oldtxt, newtxt)
        }
    }

    var renderCard = function(entries) {
        entries = shuffle(entries);
        replaceText("{numsquares}", entries.length);

        var root = document.getElementById("card");
        var table = document.createElement("table");
        var row = document.createElement("tr");
        ['B', 'I', 'N', 'G', 'O'].forEach(letter => {
            var cell = document.createElement("th");
            cell.innerHTML = letter;
            row.append(cell);
        });
        table.append(row);

        for (let row=0; row<5; row++) {
            var r = document.createElement("tr");
            for (let col=0; col<5; col++) {
                var c = document.createElement("td");
                var idx = (row*5) + col;
                if ( (row == 2) && (col == 2) ) {
                    var img = document.createElement("img");
                    img.src = "free.png";
                    c.append(img);
                } else {
                    c.innerHTML = entries[idx]['Bingo Squares'];
                }
                r.append(c)
            }
            table.append(r);
        }
        root.append(table);
    }

    function init() {
        Papa.parse('https://docs.google.com/spreadsheets/d/e/2PACX-1vR3ODoOMkDj2JquzOZYURjFiELmtjsmrYlkJuKrEmuAHkFxrtwCtq24dnBwVf6lPZ6w-rlqG7NH7zQt/pub?output=csv', {
        download: true,
        header: true,
        complete: function(results) {
            var data = results.data
            renderCard(results.data);
        }
        })
    }
    window.addEventListener('DOMContentLoaded', init);
</script>
