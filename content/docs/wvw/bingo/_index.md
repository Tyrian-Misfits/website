---
title: "Bingo!"
weight: 5
---

# Bingo!

Print this out and see if you can get bingo within the week. Refresh to generate a new card. There are currently **{numsquares}** possible squares.

To suggest new content (or to object to existing content), contact Haele (Perlkönig).

<div id="card">
</div>

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

    window.addEventListener("load", function() {
        var entries = [
            '"more tar"',
            '"get your nods"',
            'You end up blasting a non-smoke field',
            'Someone trashes Canadians',
            'Bacon is discussed',
            'Deads links any of his legendary gear',
            'More than one person falls to their death following the commander',
            'A non-English conversation happens on voice chat',
            'Deads goes on a sweary trash talk rant while killing a blob',
            'We spend five minutes or more sniffing out a thief/mesmer',
            'We win an objective after wiping at least once',
            'We overhear a private conversation over voice chat',
            'Someone (usually Maiden) blurts out an unintentional "double entendre"',
            'Someone joins the guild during the run',
            'Deads says "weeeeeeee"',
            'Someone besides tag drops siege',
            'Deads pretends to be talking behind someone\'s back',
            'Hi, Late. I\'m Deads.',
            'Tag throws wrong siege',
            'Tag sieges own objective',
            'Ba-by shark...',
            'Monkey/Akili calling tags ididots (or some variant)',
            'Deads asks for 5 gold',
            'Tag mounts up or glides while stealthed',
            'The squad becomes malnourished'
        ];
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
                    c.innerHTML = entries[idx];
                }
                r.append(c)
            }
            table.append(r);
        }
        root.append(table);
    });
</script>
