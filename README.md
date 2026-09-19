# Moodle-LNTU-Fix

# ПРАЦЮВАТИ ТІЛЬКИ ЧЕРЕЗ ДОКУМЕНТАЦІЮ ПОКРОКОВО!!! 

Встановлюємо у ваш браузер утиліту (Tampermonkey автор Jan Binio)

на базі firefox : https://addons.mozilla.org/uk/firefox/addon/tampermonkey/ 
на базі google chrome : https://chromewebstore.google.com/detail/tampermonkey/dhdgffkkebhmkfjojejmpbldmpobfkfo?hl=uk
на базі opera : https://addons.opera.com/uk/extensions/details/tampermonkey-beta/ 

Далі заходимо в

Потім нажимаємо на Create new script 

Потім після створення скрипту заміняємо стандартний скрипт на оцей 

// ==UserScript==
// @name         Moodle LNTU Fixer Simple
// @namespace    http://tampermonkey.net
// @version      2.0
// @description  Простий автоматичний фікс для ЛНТУ
// @author       imtiredwhenitalk
// @match        https://mdl.lntu.edu.ua/*
// @grant        none
// @run-at       document-end
// ==/UserScript==

(function() {
    'use strict';

    // Функція, яку ви вводили в консоль (вона 100% працює)
    function fix() {
        document.documentElement.removeAttribute('class');
        document.body.removeAttribute('class');
        document.documentElement.style = '';
        document.body.style = '';
    }

    // Запускаємо відразу при завантаженні сторінки
    fix();

    // Запускаємо повторно при БУДЬ-ЯКОМУ кліку мишкою по сайту (коли ви переходите на нову сторінку)
    document.addEventListener('click', function() {
        setTimeout(fix, 100); // чистить класи через 0.1 сек після кліку
        setTimeout(fix, 500); // підстраховка через 0.5 сек, якщо сторінка вантажиться довше
    });

    // Підстраховка при зміні адреси сайту (для AJAX переходів)
    window.addEventListener('popstate', fix);
    window.addEventListener('hashchange', fix);
})();
