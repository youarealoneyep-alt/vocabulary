<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>🌿 warm breeze · vocabulary practice</title>
    <style>
        * {
            margin: 0;
            padding: 0;
            box-sizing: border-box;
            font-family: 'Segoe UI', 'Roboto', 'Helvetica Neue', system-ui, sans-serif;
        }

        body {
            background: linear-gradient(145deg, #f9f7e8 0%, #f0efe2 100%);
            min-height: 100vh;
            padding: 2rem 1.5rem;
            display: flex;
            flex-direction: column;
            align-items: center;
            justify-content: center;
            position: relative;
            overflow-x: hidden;
        }

        /* gentle picturesque touches */
        body::before {
            content: "🌿";
            position: absolute;
            top: 20px;
            left: 30px;
            font-size: 4rem;
            opacity: 0.2;
            transform: rotate(-15deg);
            pointer-events: none;
        }

        body::after {
            content: "🕊️";
            position: absolute;
            bottom: 20px;
            right: 30px;
            font-size: 4.5rem;
            opacity: 0.15;
            transform: rotate(10deg);
            pointer-events: none;
        }

        .container {
            max-width: 1300px;
            width: 100%;
            background: rgba(255, 255, 240, 0.75);
            backdrop-filter: blur(8px);
            border-radius: 3.5rem;
            padding: 2.5rem 2rem;
            box-shadow: 0 30px 45px -20px rgba(70, 70, 50, 0.4), inset 0 1px 4px rgba(255, 255, 240, 0.8);
            border: 1px solid rgba(210, 200, 170, 0.5);
            position: relative;
            z-index: 2;
            transition: all 0.2s;
        }

        h1 {
            font-size: 2.6rem;
            font-weight: 400;
            letter-spacing: -0.02em;
            color: #3d4a2e;
            display: flex;
            align-items: center;
            gap: 12px;
            margin-bottom: 0.4rem;
            text-shadow: 2px 2px 0 #ece9d8;
            flex-wrap: wrap;
        }

        h1 span {
            background: #d9d2b6;
            padding: 0.2rem 1rem;
            border-radius: 60px;
            font-size: 1.1rem;
            font-weight: 400;
            color: #2e3b1e;
            letter-spacing: 0.3px;
            border: 1px solid #b9af8b;
            box-shadow: inset 0 1px 3px white;
        }

        .subhead {
            display: flex;
            justify-content: space-between;
            align-items: center;
            margin-bottom: 1.8rem;
            flex-wrap: wrap;
            gap: 15px;
            border-bottom: 2px dashed #ccc7a8;
            padding-bottom: 0.9rem;
        }

        .progress-badge {
            background: #b7b28b;
            color: #242b15;
            padding: 0.5rem 1.3rem;
            border-radius: 80px;
            font-weight: 500;
            font-size: 0.95rem;
            box-shadow: 0 2px 5px rgba(0, 0, 0, 0.05), inset 0 1px 3px #ded9bb;
            border: 1px solid #a9a17b;
        }

        .btn-reset {
            background: transparent;
            border: 1.5px solid #b1a984;
            color: #494e2e;
            padding: 0.5rem 1.3rem;
            border-radius: 40px;
            font-weight: 500;
            cursor: pointer;
            transition: all 0.2s;
            font-size: 0.95rem;
            display: flex;
            align-items: center;
            gap: 6px;
        }

        .btn-reset:hover {
            background: #dad3b6;
            border-color: #8e865f;
            transform: scale(1.02);
            box-shadow: 0 4px 10px rgba(100, 90, 50, 0.1);
        }

        .btn-reset:active {
            transform: scale(0.98);
        }

        .card-grid {
            display: grid;
            grid-template-columns: repeat(auto-fill, minmax(300px, 1fr));
            gap: 1.2rem;
            margin-top: 1rem;
        }

        .card {
            background: #fdfdf5;
            border-radius: 2rem 2rem 2rem 2rem;
            padding: 1.2rem 1.2rem 1.3rem 1.2rem;
            box-shadow: 0 10px 18px -10px rgba(80, 75, 40, 0.2), 0 0 0 1px #eae5cf, 0 0 0 2px #f8f6ea inset;
            transition: all 0.2s ease;
            display: flex;
            flex-direction: column;
            border-left: 7px solid #b9c28b;
            cursor: pointer;
            position: relative;
            user-select: none;
        }

        .card:hover {
            transform: translateY(-4px);
            box-shadow: 0 20px 25px -12px #a8a27b, 0 0 0 1px #cbc4a4, 0 0 0 2px #fefcf0 inset;
            background: #fffffc;
        }

        .card.revealed {
            border-left-color: #9bb87a;
            background: #f8fbea;
        }

        .card.revealed .answer {
            opacity: 1;
            max-height: 200px;
            margin-top: 0.6rem;
            padding-top: 0.6rem;
            border-top: 1px dashed #c6c2a2;
        }

        .word {
            font-size: 1.3rem;
            font-weight: 600;
            color: #3b4426;
            letter-spacing: -0.3px;
            display: flex;
            align-items: center;
            gap: 8px;
            flex-wrap: wrap;
        }

        .word .emoji {
            font-size: 1.5rem;
            filter: drop-shadow(0 2px 2px rgba(0,0,0,0.05));
        }

        .hint {
            font-size: 0.9rem;
            color: #817b58;
            margin-top: 0.35rem;
            font-style: italic;
            display: flex;
            align-items: center;
            gap: 6px;
            margin-bottom: 0.4rem;
        }

        .hint::before {
            content: "👆";
            font-size: 0.9rem;
            opacity: 0.7;
            font-style: normal;
        }

        .card.revealed .hint::before {
            content: "🔍";
        }

        .answer {
            opacity: 0;
            max-height: 0;
            overflow: hidden;
            transition: opacity 0.3s ease, max-height 0.35s ease, margin 0.2s, padding 0.2s;
            color: #2c3820;
            font-size: 0.95rem;
            line-height: 1.5;
            background: #f1f2e2;
            border-radius: 1.2rem;
            padding: 0 0.8rem;
            margin-top: 0;
        }

        .card.revealed .answer {
            padding: 0.7rem 0.8rem;
            margin-top: 0.5rem;
            opacity: 1;
            max-height: 200px;
        }

        .answer p {
            background: #e9ecd9;
            padding: 0.5rem 0.8rem;
            border-radius: 1rem;
            color: #2d3921;
            font-weight: 450;
            border: 1px solid #d6d6b8;
            box-shadow: inset 0 1px 2px white;
        }

        .example {
            font-size: 0.85rem;
            color: #5a6242;
            margin-top: 0.4rem;
            font-style: italic;
            display: flex;
            gap: 5px;
        }

        .example::before {
            content: "✧";
            color: #b3ab7a;
        }

        /* footer */
        .footer-note {
            margin-top: 2.5rem;
            text-align: center;
            color: #8e8a6b;
            font-size: 0.85rem;
            font-weight: 400;
            letter-spacing: 0.3px;
            display: flex;
            justify-content: center;
            gap: 20px;
            flex-wrap: wrap;
            border-top: 1px solid #dfdbc0;
            padding-top: 1.5rem;
        }

        .footer-note span {
            background: #eae7d3;
            padding: 0.3rem 1rem;
            border-radius: 50px;
            color: #585b3e;
        }

        /* responsive */
        @media (max-width: 650px) {
            body { padding: 1rem; }
            .container { padding: 1.5rem; }
            h1 { font-size: 1.9rem; }
            .card-grid { grid-template-columns: 1fr; }
            .word { font-size: 1.2rem; }
        }
    </style>
</head>
<body>
    <div class="container">
        <h1>
            📖 warm breeze · word practice
            <span>32 expressions</span>
        </h1>
        <div class="subhead">
            <div class="progress-badge" id="progressBadge">✨ 0 / 32 revealed</div>
            <button class="btn-reset" id="resetBtn">🔄 reset all cards</button>
        </div>

        <div class="card-grid" id="cardGrid">
            <!-- cards will be injected with JS -->
        </div>

        <div class="footer-note">
            <span>🌱 click any card to reveal meaning & example</span>
            <span>🧘 learn at your own pace</span>
        </div>
    </div>

    <script>
        (function() {
            // --------------------------------------------------------------
            // 1. Data: all 32 vocabulary entries with word, definition, example
            // --------------------------------------------------------------
            const vocabData = [
                { word: "warm breeze", def: "a gentle, mild wind", example: "A warm breeze drifted through the open window." },
                { word: "sway", def: "to move slowly and rhythmically from side to side", example: "The palm trees sway in the tropical wind." },
                { word: "breathe in", def: "to inhale deeply; to take air into the lungs", example: "Breathe in the fresh mountain air." },
                { word: "shine", def: "to reflect light; to glow brightly", example: "The sun began to shine after the rain." },
                { word: "grey clouds fill the sky", def: "a descriptive phrase for a gloomy day", example: "Grey clouds fill the sky, promising rain." },
                { word: "squash together", def: "to press tightly into a small space", example: "We had to squash together in the back seat." },
                { word: "ache", def: "to experience a continuous dull pain", example: "My muscles ache after the long hike." },
                { word: "flat grasslands", def: "wide, open areas of land covered in grass", example: "The savanna is full of flat grasslands." },
                { word: "beat down", def: "(of the sun) to shine very strongly and hotly", example: "The sun beat down on the desert." },
                { word: "cloudless sky", def: "a sky with no clouds; completely clear", example: "Under a cloudless sky, the stars were brilliant." },
                { word: "cicadas", def: "insects that make a loud, high-pitched buzzing sound in hot weather", example: "The cicadas sang all through the summer night." },
                { word: "fill my nostrils", def: "to describe a very strong smell entering your nose", example: "The scent of jasmine filled my nostrils." },
                { word: "when you least expect it", def: "when you are not anticipating or planning for something", example: "Happiness arrives when you least expect it." },
                { word: "end up in", def: "to finally arrive somewhere, usually without planning to", example: "We got lost and ended up in a tiny village." },
                { word: "just for an instant", def: "for a very short moment", example: "Just for an instant, I thought I saw a deer." },
                { word: "like books on a shelf", def: "a simile used to describe people packed tightly together", example: "The commuters stood like books on a shelf." },
                { word: "feel a bit numb", def: "to feel emotionally empty or unable to feel anything", example: "After the news, I felt a bit numb." },
                { word: "be grateful for", def: "to feel thankful for something", example: "I am grateful for your kindness." },
                { word: "take my breath away", def: "an idiom meaning something was incredibly beautiful or amazing", example: "The view from the cliff took my breath away." },
                { word: "bustling", def: "a word to describe a very busy, active place", example: "The bustling market was full of colors and noise." },
                { word: "sway like dancers", def: "to move gracefully like a dancer", example: "The flowers sway like dancers in the breeze." },
                { word: "be squashed together like books on a shelf", def: "to be packed very tightly", example: "In the elevator we were squashed together like books on a shelf." },
                { word: "feel like being roasted in an oven", def: "to feel extremely hot", example: "Without air conditioning, I felt like being roasted in an oven." },
                { word: "cicadas sing", def: "personification of insects making noise", example: "The cicadas sing in the heat of July." },
                { word: "happiness happens when", def: "starting a general statement about a concept", example: "Happiness happens when you stop comparing yourself." },
                { word: "believe that", def: "to express a personal opinion", example: "I believe that kindness changes the world." },
                { word: "as the train comes into", def: "setting a scene with simultaneous actions", example: "As the train comes into the station, people gather their bags." },
                { word: "realise at that moment that", def: "to express a sudden realization", example: "I realise at that moment that I forgot my keys." },
                { word: "think about things to be grateful for", def: "to list things you are thankful for", example: "Every night, think about things to be grateful for." },
                { word: "how can you not be happy in a place like this", def: "using a rhetorical question to express emotion", example: "With such beauty, how can you not be happy in a place like this?" },
                { word: "cicadas", def: "insects that make a loud, high-pitched buzzing sound in hot weather", example: "The cicadas' buzz is the soundtrack of summer." },      // duplicate but distinct entry
                { word: "warm breeze", def: "a gentle, mild wind", example: "The warm breeze carried the scent of pine." }                                      // duplicate (same word, extra example)
            ];

            // Note: we have 32 entries exactly? Let's count: 
            // 30 unique from first list (including duplicates as per provided) but we need 32, 
            // we added 2 more (cicadas duplicate and warm breeze duplicate) → total 32.
            // but we'll ensure exactly 32 cards are displayed. 
            // Actually let's recount our data: from the user's list, there are 30 lines? 
            // Let's list the original user list: (copy-paste)
            // warm breeze, sway, breathe in, shine, grey clouds fill the sky, squash together, ache, flat grasslands, beat down, cloudless sky, cicadas, fill my nostrils, when you least expect it, end up in, just for an instant, like books on a shelf, feel a bit numb, be grateful for, take my breath away, bustling, sway like dancers, be squashed together like books on a shelf, feel like being roasted in an oven, cicadas sing, happiness happens when, believe that, as the train comes into, realise at that moment that, think about things to be grateful for, how can you not be happy in a place like this → 30 entries.
            // But the description says "32 expressions". So we add two more natural extensions? 
            // We'll add: "warm breeze" (second example) and "cicadas" (second example) – they appear naturally.
            // That makes 32. Perfect.

            // Let's ensure we have exactly 32 entries.
            // We'll adjust our vocabData above to have 32 items. 
            // Count above: index 0 to 31 = 32 items. Good.
            // But we had a duplicate 'cicadas' and duplicate 'warm breeze' — that's fine.
            // We'll sort? No need. But we want clean.
            // Let's rebuild properly with 32 items for clarity.

            // Rebuild data (final) with exactly 32 entries, no duplicate word unless intended.
            // I'll create a final array with 32 items, using the user's list + 2 extra (second cicadas & second warm breeze).
            // For better UX, we can slightly vary the wording on the extra ones? But we keep as is.

            const finalVocab = [
                { word: "warm breeze", def: "a gentle, mild wind", example: "A warm breeze drifted through the open window." },
                { word: "sway", def: "to move slowly and rhythmically from side to side", example: "The palm trees sway in the tropical wind." },
                { word: "breathe in", def: "to inhale deeply; to take air into the lungs", example: "Breathe in the fresh mountain air." },
                { word: "shine", def: "to reflect light; to glow brightly", example: "The sun began to shine after the rain." },
                { word: "grey clouds fill the sky", def: "a descriptive phrase for a gloomy day", example: "Grey clouds fill the sky, promising rain." },
                { word: "squash together", def: "to press tightly into a small space", example: "We had to squash together in the back seat." },
                { word: "ache", def: "to experience a continuous dull pain", example: "My muscles ache after the long hike." },
                { word: "flat grasslands", def: "wide, open areas of land covered in grass", example: "The savanna is full of flat grasslands." },
                { word: "beat down", def: "(of the sun) to shine very strongly and hotly", example: "The sun beat down on the desert." },
                { word: "cloudless sky", def: "a sky with no clouds; completely clear", example: "Under a cloudless sky, the stars were brilliant." },
                { word: "cicadas", def: "insects that make a loud, high-pitched buzzing sound in hot weather", example: "The cicadas sang all through the summer night." },
                { word: "fill my nostrils", def: "to describe a very strong smell entering your nose", example: "The scent of jasmine filled my nostrils." },
                { word: "when you least expect it", def: "when you are not anticipating or planning for something", example: "Happiness arrives when you least expect it." },
                { word: "end up in", def: "to finally arrive somewhere, usually without planning to", example: "We got lost and ended up in a tiny village." },
                { word: "just for an instant", def: "for a very short moment", example: "Just for an instant, I thought I saw a deer." },
                { word: "like books on a shelf", def: "a simile used to describe people packed tightly together", example: "The commuters stood like books on a shelf." },
                { word: "feel a bit numb", def: "to feel emotionally empty or unable to feel anything", example: "After the news, I felt a bit numb." },
                { word: "be grateful for", def: "to feel thankful for something", example: "I am grateful for your kindness." },
                { word: "take my breath away", def: "an idiom meaning something was incredibly beautiful or amazing", example: "The view from the cliff took my breath away." },
                { word: "bustling", def: "a word to describe a very busy, active place", example: "The bustling market was full of colors and noise." },
                { word: "sway like dancers", def: "to move gracefully like a dancer", example: "The flowers sway like dancers in the breeze." },
                { word: "be squashed together like books on a shelf", def: "to be packed very tightly", example: "In the elevator we were squashed together like books on a shelf." },
                { word: "feel like being roasted in an oven", def: "to feel extremely hot", example: "Without air conditioning, I felt like being roasted in an oven." },
                { word: "cicadas sing", def: "personification of insects making noise", example: "The cicadas sing in the heat of July." },
                { word: "happiness happens when", def: "starting a general statement about a concept", example: "Happiness happens when you stop comparing yourself." },
                { word: "believe that", def: "to express a personal opinion", example: "I believe that kindness changes the world." },
                { word: "as the train comes into", def: "setting a scene with simultaneous actions", example: "As the train comes into the station, people gather their bags." },
                { word: "realise at that moment that", def: "to express a sudden realization", example: "I realise at that moment that I forgot my keys." },
                { word: "think about things to be grateful for", def: "to list things you are thankful for", example: "Every night, think about things to be grateful for." },
                { word: "how can you not be happy in a place like this", def: "using a rhetorical question to express emotion", example: "With such beauty, how can you not be happy in a place like this?" },
                { word: "cicadas (buzzing)", def: "insects that make a loud, high-pitched buzzing sound in hot weather", example: "The cicadas' buzz is the soundtrack of summer." },     // extra 31
                { word: "warm breeze (soft wind)", def: "a gentle, mild wind", example: "The warm breeze carried the scent of pine." }                                      // extra 32
            ];

            // Ensure we have exactly 32
            // If for any reason it's less, we'll slice, but it's 32.

            // --------------------------------------------------------------
            // 2. Render cards
            // --------------------------------------------------------------
            const grid = document.getElementById('cardGrid');
            const progressBadge = document.getElementById('progressBadge');
            let revealedCount = 0;
            const totalCards = finalVocab.length; // should be 32

            // Store card elements to update progress
            const cardElements = [];

            // Helper to update progress badge
            function updateProgress() {
                progressBadge.textContent = `✨ ${revealedCount} / ${totalCards} revealed`;
            }

            // Clear grid
            grid.innerHTML = '';

            // Create each card
            finalVocab.forEach((item, index) => {
                const card = document.createElement('div');
                card.className = 'card';
                // store index to toggle
                card.dataset.index = index;

                // Word with optional emoji accent
                const wordDiv = document.createElement('div');
                wordDiv.className = 'word';
                // add a little natural emoji touch based on some words? (optional)
                let emoji = '🌿';
                if (item.word.includes('sun') || item.word.includes('shine') || item.word.includes('beat')) emoji = '☀️';
                else if (item.word.includes('cicada')) emoji = '🦗';
                else if (item.word.includes('cloud')) emoji = '☁️';
                else if (item.word.includes('breeze') || item.word.includes('sway')) emoji = '🍃';
                else if (item.word.includes('breath')) emoji = '💨';
                else if (item.word.includes('grateful') || item.word.includes('happiness')) emoji = '😊';
                else if (item.word.includes('book')) emoji = '📚';
                else if (item.word.includes('train')) emoji = '🚆';
                else if (item.word.includes('bustling')) emoji = '🏙️';
                else if (item.word.includes('oven') || item.word.includes('roasted')) emoji = '🔥';
                else if (item.word.includes('ache') || item.word.includes('numb')) emoji = '💭';
                else if (item.word.includes('grass')) emoji = '🌾';
                else emoji = '✨';
                
                wordDiv.innerHTML = `${emoji} ${item.word}`;
                card.appendChild(wordDiv);

                // hint
                const hintDiv = document.createElement('div');
                hintDiv.className = 'hint';
                hintDiv.textContent = 'click to reveal meaning';
                card.appendChild(hintDiv);

                // answer (hidden initially)
                const answerDiv = document.createElement('div');
                answerDiv.className = 'answer';
                answerDiv.innerHTML = `<p>${item.def}</p>`;
                // add example inside answer block
                const exampleDiv = document.createElement('div');
                exampleDiv.className = 'example';
                exampleDiv.textContent = item.example;
                answerDiv.appendChild(exampleDiv);
                card.appendChild(answerDiv);

                // click toggle
                card.addEventListener('click', (e) => {
                    // Prevent toggling if clicking a button? no
                    const isRevealed = card.classList.contains('revealed');
                    if (isRevealed) {
                        card.classList.remove('revealed');
                        revealedCount--;
                    } else {
                        card.classList.add('revealed');
                        revealedCount++;
                    }
                    updateProgress();
                });

                // store element for reset
                cardElements.push({ card, answerDiv, hintDiv });
                grid.appendChild(card);
            });

            // initial progress
            updateProgress();

            // reset button
            document.getElementById('resetBtn').addEventListener('click', () => {
                cardElements.forEach(({ card }) => {
                    card.classList.remove('revealed');
                });
                revealedCount = 0;
                updateProgress();
            });

            // optional: keyboard or extra touches? not needed

            // add a tiny picturesque detail: random soft background element
            // no extra needed

            // ensure progress counts if user reveals all
            // also handle if something gets out of sync: we recompute from cards on reset.
            // but we keep revealedCount consistent via event listeners.
            // However if someone double-clicks quickly, but fine.

            // Edge: if we remove all revealed and then toggle, count is synced.
            // We can also add a check function, but fine.

            // smooth: if progress becomes 0, that's fine.
        })();
    </script>
</body>
</html>
