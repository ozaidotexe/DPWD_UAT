// ==UserScript==
// @name         [LC x WD] ID Pantau (Cloud Sync + Livechat Announce)
// @namespace    http://tampermonkey.net/
// @version      4.9.5
// @description  Manajemen ID Pantau dengan Optimasi Performa & Anti-Delay
// @author       Lord Ozai
// @match        https://raj.1lg878-596l.com/adm/withdrawal
// @match        https://raj.1lg878-596l.com/adm/withdrawal?bank_lists_id=*
// @grant        GM_xmlhttpRequest
// @connect      api.github.com
// @run-at       document-idle
// ==/UserScript==

(function() {
    'use strict';

    const GITHUB_TOKEN = "ghp_vWZkHIspToiHxcpsooz2gKlplDm5YJ2C7v7c"; // <<<------ Rubah code "7c" menjadi "4r"
    const GIST_ID = "27aa477e92cfce1bc0a873d02a7d6e28";
    const FILE_WATCHLIST = "watchlist_wd.json";
    const FILE_PRIORITY = "priority_wd.json";

    let IS_UPLOADING = false;
    let PLAYED_ALARMS = new Set();

    const AUDIO_ALERT = new Audio('https://assets.mixkit.co/active_storage/sfx/2869/2869-600.wav');

    // Inject CSS Global Sekali Saja di Awal
    if (!document.getElementById('blink-style')) {
        const style = document.createElement('style');
        style.id = 'blink-style';
        style.innerHTML = `
            @keyframes blinker { 50% { opacity: 0.3; } }
            .lc-tag:after { content: attr(data-text); }
        `;
        document.head.appendChild(style);
    }

    function getWatchlist() {
        const saved = localStorage.getItem('WATCHLIST_DATA');
        return saved ? JSON.parse(saved).map(u => u.toUpperCase()) : [];
    }

    function getPriorityList() {
        const saved = localStorage.getItem('PRIORITY_DATA');
        return saved ? JSON.parse(saved).map(u => u.toUpperCase()) : [];
    }

    // ==========================================
    // CLOUD SYNC & FETCH LOGIC
    // ==========================================
    function fetchCloudData() {
        if (!GIST_ID || !GITHUB_TOKEN || IS_UPLOADING) return;

        GM_xmlhttpRequest({
            method: "GET",
            url: `https://api.github.com/gists/${GIST_ID}`,
            headers: {
                "Authorization": `token ${GITHUB_TOKEN}`,
                "Accept": "application/vnd.github.v3+json",
                "Cache-Control": "no-cache"
            },
            onload: function(response) {
                if (IS_UPLOADING || response.status !== 200) return;

                try {
                    const data = JSON.parse(response.responseText);
                    let needHighlight = false;

                    if (data.files && data.files[FILE_WATCHLIST]) {
                        const cloudList = JSON.parse(data.files[FILE_WATCHLIST].content).map(id => id.toUpperCase());
                        if (localStorage.getItem('WATCHLIST_DATA') !== JSON.stringify(cloudList)) {
                            localStorage.setItem('WATCHLIST_DATA', JSON.stringify(cloudList));
                            needHighlight = true;
                        }
                    }

                    if (data.files && data.files[FILE_PRIORITY]) {
                        const cloudPriority = JSON.parse(data.files[FILE_PRIORITY].content).map(id => id.toUpperCase());
                        if (localStorage.getItem('PRIORITY_DATA') !== JSON.stringify(cloudPriority)) {
                            localStorage.setItem('PRIORITY_DATA', JSON.stringify(cloudPriority));
                            needHighlight = true;
                        }
                    }

                    if (needHighlight) highlightWatchlist();

                } catch(e) {
                    console.error("Gagal parse data cloud:", e);
                }
            }
        });
    }

    function saveCloudData(fileName, cleanList) {
        if (!GIST_ID || !GITHUB_TOKEN) return;
        IS_UPLOADING = true;

        const bodyData = {
            description: "Updated via Tampermonkey v4.9.5",
            files: {}
        };
        bodyData.files[fileName] = { content: JSON.stringify(cleanList) };

        GM_xmlhttpRequest({
            method: "PATCH",
            url: `https://api.github.com/gists/${GIST_ID}`,
            headers: {
                "Authorization": `token ${GITHUB_TOKEN}`,
                "Accept": "application/vnd.github.v3+json",
                "Content-Type": "application/json"
            },
            data: JSON.stringify(bodyData),
            onload: function(response) {
                // Selesai upload langsung ubah status tanpa delay buatan yang lama
                IS_UPLOADING = false;
                if (response.status === 200) {
                    console.log(`Cloud Sync Success [${fileName}]`);
                }
            },
            onerror: function() { IS_UPLOADING = false; }
        });
    }

    // Interval fetch ditingkatkan ke 7 detik untuk menghindari Rate Limit GitHub API
    fetchCloudData();
    setInterval(fetchCloudData, 7000);

    // ==========================================
    // INTERFACE / UI MANAGEMENT
    // ==========================================
    function createControlPanel() {
        if (document.getElementById('wd-control-panel')) return;

        const cardHeaders = document.querySelectorAll('.card-header, .box-header, .panel-heading');
        let targetHeader = null;

        for (let header of cardHeaders) {
            if (header.textContent.includes('Withdrawal Baru')) {
                targetHeader = header;
                break;
            }
        }

        if (!targetHeader) {
            const table = document.querySelector('table');
            if (table && table.parentElement) {
                const parent = table.closest('.card, .box, .panel') || table.parentElement;
                targetHeader = parent.querySelector('.card-header, .box-header, div[class*="header"]');
            }
        }

        const panelTop = document.createElement('div');
        panelTop.id = 'wd-control-panel-top';
        panelTop.style = `display: flex; margin-left: auto;`;

        const btnLC = document.createElement('button');
        btnLC.innerHTML = '📢 LiveChat: ID Priority';
        btnLC.style = `padding: 6px 12px; background: #E67E22; color: white; border: none;
                       border-radius: 4px; cursor: pointer; font-weight: bold; font-size: 13px; box-shadow: 0 2px 4px rgba(0,0,0,0.15);`;
        btnLC.onclick = function() {
            const input = prompt("MASUKKAN ID dari LIVECHAT (Lepas Pantau / Minta WD Cepat):\n\n*Gunakan koma (,) Jika lebih dari 1 ID");
            if (input) {
                let items = input.split(',').map(i => i.trim().toUpperCase());
                let currentPriority = getPriorityList();
                let newPriority = [...new Set([...currentPriority, ...items])];

                localStorage.setItem('PRIORITY_DATA', JSON.stringify(newPriority));
                highlightWatchlist(); // Instan update visual tanpa delay
                saveCloudData(FILE_PRIORITY, newPriority);
                alert("ID Berhasil dikirim ke anak WD!");
            }
        };

        panelTop.appendChild(btnLC);

        if (targetHeader) {
            targetHeader.style.display = 'flex';
            targetHeader.style.justifyContent = 'space-between';
            targetHeader.style.alignItems = 'center';
            targetHeader.appendChild(panelTop);
        } else {
            panelTop.style = `position: fixed; bottom: 70px; right: 20px; z-index: 9999;`;
            document.body.appendChild(panelTop);
        }

        const panelBottom = document.createElement('div');
        panelBottom.id = 'wd-control-panel';
        panelBottom.style = `position: fixed; bottom: 20px; right: 20px; z-index: 9999;`;

        const btnWD = document.createElement('button');
        btnWD.innerHTML = '⚙️ Kelola ID Pantau [Cloud]';
        btnWD.style = `padding: 10px 15px; background: #05203D; color: white; border: none;
                       border-radius: 5px; cursor: pointer; font-weight: bold; box-shadow: 0 4px 6px rgba(0,0,0,0.2);`;
        btnWD.onclick = function() {
            const currentList = getWatchlist();
            const input = prompt(
                "DAFTAR ID PANTAU SAAT INI (" + currentList.length + " ID):\n" +
                currentList.join(", ") +
                "\n\n- Ketik ID untuk TAMBAH atau HAPUS\n- Gunakan koma (,) untuk banyak ID sekaligus"
            );

            if (input !== null && input.trim() !== "") {
                let items = input.split(',').map(i => i.trim().toUpperCase());
                let newList = [...currentList];
                items.forEach(item => {
                    if (newList.includes(item)) {
                        newList = newList.filter(id => id !== item);
                    } else {
                        newList.push(item);
                    }
                });
                localStorage.setItem('WATCHLIST_DATA', JSON.stringify(newList));
                highlightWatchlist(); // Instan update visual tanpa delay
                saveCloudData(FILE_WATCHLIST, newList);
            }
        };

        panelBottom.appendChild(btnWD);
        document.body.appendChild(panelBottom);
    }

    // ==========================================
    // HIGHLIGHT & DETEKSI PRIORITAS
    // ==========================================
    function highlightWatchlist() {
        const WATCHLIST = getWatchlist();
        const PRIORITY_LIST = getPriorityList();
        const rows = document.querySelectorAll('table tbody tr');

        rows.forEach((row) => {
            const usernameCell = row.cells[2];
            const toBankCell = row.cells[4];
            const actionCell = row.cells[6];

            if (!usernameCell || !toBankCell) return;

            const currentUsername = usernameCell.textContent.replace(/⏳ PRIORITAS! \[<5m\]/g, '').trim().toUpperCase();

            // 1. KONDISI: ID PRIORITAS DARI LIVECHAT
            if (PRIORITY_LIST.includes(currentUsername)) {
                if (usernameCell.style.backgroundColor !== '') {
                    usernameCell.style.backgroundColor = '';
                    usernameCell.style.color = '';
                    usernameCell.style.fontWeight = '';
                }

                if (!PLAYED_ALARMS.has(currentUsername)) {
                    AUDIO_ALERT.play().catch(e => console.log("Izin audio browser aktif"));
                    PLAYED_ALARMS.add(currentUsername);
                }

                if (!usernameCell.querySelector('.lc-tag')) {
                    const tag = document.createElement('span');
                    tag.className = 'lc-tag';
                    tag.setAttribute('data-text', '⏳ PRIORITAS! [<5m]');
                    tag.style = 'margin-left: 8px; padding: 2px 6px; background: red; color: white; border-radius: 3px; font-size: 10px; font-weight: bold; display: inline-block; vertical-align: middle; animation: blinker 1s linear infinite; user-select: none; -webkit-user-select: none;';
                    usernameCell.appendChild(tag);
                }

                if (actionCell && !actionCell.querySelector('.btn-done-wd')) {
                    const btnDone = document.createElement('button');
                    btnDone.className = 'btn-done-wd';
                    btnDone.innerText = '✅ Selesai?';
                    btnDone.style = 'margin-left: 5px; padding: 6px 10px; font-size: 12px; font-weight: bold; background: #2ECC71; color: white; border: none; border-radius: 4px; cursor: pointer; height: 32px; vertical-align: middle;';

                    btnDone.onclick = function(e) {
                        e.stopPropagation();

                        if (confirm(`Hapus ${currentUsername} dari antrean prioritas < 5 menit ? \n\n*Jangan lupa lepaskan ID PANTAU setelah selesai!\n*Konfirmasi kembali ke Team Livechat!`)) {
                            let updatedPriority = getPriorityList().filter(id => id !== currentUsername);
                            localStorage.setItem('PRIORITY_DATA', JSON.stringify(updatedPriority));
                            PLAYED_ALARMS.delete(currentUsername);

                            // Langsung hapus elemen saat diklik (Hapus delay visual)
                            if(usernameCell.querySelector('.lc-tag')) usernameCell.querySelector('.lc-tag').remove();
                            btnDone.remove();

                            usernameCell.style.backgroundColor = '';
                            usernameCell.style.color = '';
                            usernameCell.style.fontWeight = '';

                            saveCloudData(FILE_PRIORITY, updatedPriority);
                            highlightWatchlist(); // Refresh posisi status baris secara instan
                        }
                    };
                    actionCell.appendChild(btnDone);
                }
            }

            else if (WATCHLIST.includes(currentUsername)) {
                if (usernameCell.style.backgroundColor !== 'rgb(255, 204, 204)') {
                    usernameCell.style.backgroundColor = '#ffcccc';
                    usernameCell.style.color = '#cc0000';
                    usernameCell.style.fontWeight = '900';
                    toBankCell.style.color = '#ff0000';
                    toBankCell.style.fontWeight = 'bold';
                }

                if(usernameCell.querySelector('.lc-tag')) usernameCell.querySelector('.lc-tag').remove();
                if(actionCell && actionCell.querySelector('.btn-done-wd')) actionCell.querySelector('.btn-done-wd').remove();
            }

            else {
                if (usernameCell.style.backgroundColor !== '') {
                    usernameCell.style.backgroundColor = '';
                    usernameCell.style.color = '';
                    usernameCell.style.fontWeight = '';
                    if(usernameCell.querySelector('.lc-tag')) usernameCell.querySelector('.lc-tag').remove();
                    if(actionCell && actionCell.querySelector('.btn-done-wd')) actionCell.querySelector('.btn-done-wd').remove();
                }
            }
        });
    }

    createControlPanel();
    setInterval(highlightWatchlist, 3000);
    highlightWatchlist();
})();
