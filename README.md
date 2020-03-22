## Download health insurance claims from Aetna
This tool downloads and stores in an Excel spreadsheet the health insurance claims from Aetna (https://health.aetna.com/).

## Usage

1. Install the following GreaseMonkey script:

```js
// ==UserScript==
// @name         aetna_claims_download
// @match        https://health.aetna.com/*
// @grant        GM_setValue
// @grant        GM_getValue
// ==/UserScript==

(function() {
    'use strict';
    if (document.location.pathname != '/login_callback.html') {
        return;
    }

    var hash = document.location.hash;
    console.log(hash);
    if (hash.length > 0) {
        window.setInterval(function() {
            var div = document.createElement('div');
            var input = document.createElement('input');
            div.style = 'height: 30px; background: #ccc;position: absolute;left: 10px;top: 10px;right: 10px;';
            input.style = 'width: 95%;border: 0;display: block;margin: 5px auto';
            input.value = hash;
            input.addEventListener('click', function() {
                input.select();
            });
            div.appendChild(input);
            window.parent.document.querySelector('body').appendChild(div);
        }, 10000);
    }
})();
```

2. Modify the `FIREFOX_PROFILE_PATH` and `AETNA_MEMBER_ID` variables.

3. Login to https://health.aetna.com/.

4. Copy the tokens that will appear on the top of the page.

5. Execute the tool and paste the tokens.
